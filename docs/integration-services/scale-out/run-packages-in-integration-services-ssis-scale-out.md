---
title: SQL Server Integration Services (SSIS) Scale Out でパッケージを実行する | Microsoft Docs
description: さまざまな方法を使用して Scale Out で SQL Server Integration Services (SSIS) パッケージを実行する方法について説明します。
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
author: HaoQian-MS
ms.author: haoqian
ms.reviewer: maghan
f1_keywords:
- sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.openlocfilehash: 25f550f711364760de9cc07608b46532cfa34219
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101839016"
---
# <a name="run-packages-in-integration-services-ssis-scale-out"></a>Integration Services (SSIS) Scale Out でパッケージを実行する

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Integration Services サーバーにパッケージを配置すると、次のいずれかの方法を使用して Scale Out でそれらのパッケージを実行できます。

-   [[Scale Out でパッケージを実行] ダイアログ ボックス](#scale_out_dialog)

-   [ストアド プロシージャ](#stored_proc)

-   [SQL Server エージェント ジョブ](#sql_agent)

## <a name="run-packages-with-the-execute-package-in-scale-out-dialog-box"></a><a name="scale_out_dialog"></a> [Scale Out でパッケージを実行] ダイアログ ボックスを使用してパッケージを実行する

1. [Scale Out でパッケージを実行] ダイアログ ボックスを開きます。

    [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)]で、Integration Services サーバーに接続します。 オブジェクト エクスプローラーで、ツリーを展開し、 **[Integration Services カタログ]** のノードを表示します。 **SSISDB** ノード、プロジェクト、または実行するパッケージを右クリックし、 **[Execute in Scale Out (Scale Out で実行)]** をクリックします。

2. パッケージを選択してオプションを設定します。

    **[パッケージの選択内容]** ページで、実行するパッケージを 1 つまたは複数選択します。 環境、パラメーター、接続マネージャー、および詳細設定オプションをパッケージごとに設定します。 これらのオプションを設定するには、パッケージをクリックします。
    
    **[詳細設定]** タブで、 **[再試行回数]** と呼ばれる Scale Out オプションを設定して、パッケージが失敗した場合のパッケージの再試行回数を指定します。

    > [!NOTE]
    > Scale Out Worker サービスを実行しているアカウントがローカル コンピューターの管理者である場合、 **[エラー時にダンプする]** オプションのみが機能します。

3. worker コンピューターを選択します。

    **[マシンの選択]** ページで、パッケージを実行する Scale Out Worker コンピューターを選択します。 既定では、任意のコンピューターでパッケージを実行できます。 

   > [!NOTE] 
   > パッケージは、Scale Out Worker サービスのユーザー アカウント資格情報で実行されます。 **[マシンの選択]** ページでそれらの資格情報を確認します。 既定では、アカウントは `NT Service\SSISScaleOutWorker140` です。

   > [!WARNING]
   > パッケージの実行が同じ worker 上のさまざまなユーザーによってトリガーされる場合、同じ資格情報で実行されます。 それらの間にセキュリティ境界はありません。 

4. パッケージを実行してレポートを表示します。

    パッケージの実行を開始するには、 **[OK]** をクリックします。 パッケージの実行レポートを表示するには、オブジェクト エクスプローラーでパッケージを右クリックし、 **[レポート]** 、 **[すべての実行]** の順にクリックして実行を見つけます。
    
## <a name="run-packages-with-stored-procedures"></a><a name="stored_proc"></a> ストアド プロシージャでパッケージを実行する

1.  実行を作成します。

    パッケージごとに `[catalog].[create_execution]` を呼び出します。 パラメーター **\@runinscaleout**  を `True` に設定します。 一部の Scale Out Worker コンピューターでパッケージを実行できない場合は、パラメーター **\@useanyworker** を `False` に設定します。 このストアド プロシージャと **\@useanyworker** パラメーターの詳細については、「[catalog.create_execution](../system-stored-procedures/catalog-create-execution-ssisdb-database.md)」を参照してください。 

2. 実行パラメーターを設定します。

    実行のたびに `[catalog].[set_execution_parameter_value]` を呼び出します。

3. Scale Out Worker を設定します。

    `[catalog].[add_execution_worker]` を呼び出します。 すべてのコンピューターでパッケージを実行できる場合は、このストアド プロシージャを呼び出す必要はありません。 

4. 実行を開始します。

    `[catalog].[start_execution]` を呼び出します。 パッケージの実行が失敗した場合に再試行される回数を、パラメーター **\@retry_count** で設定します。
    
### <a name="example"></a>例
次の例では、1 つの Scale Out Worker を使用して、Scale Out で `package1.dtsx` および `package2.dtsx` という 2 つのパッケージを実行します。  

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO

Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO
```

### <a name="permissions"></a>アクセス許可
Scale Out でパッケージを実行するには、次のアクセス許可のいずれかが必要です。

-   **ssis_admin** データベース ロールのメンバーシップ  

-   **ssis_cluster_executor** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  

## <a name="set-default-execution-mode"></a>既定の実行モードを設定する
パッケージの既定の実行モードを **[Scale Out]** に設定するには、以下の操作を行います。

1.  SSMS のオブジェクト エクスプローラーで、**SSISDB** ノードを右クリックし、 **[プロパティ]** を選択します。

2.  **[カタログ プロパティ]** ダイアログ ボックスで、 **[サーバー全体の既定の実行モード]** を **[Scale Out]** に設定します。

この既定の実行モードを設定したら、`[catalog].[create_execution]` ストアド プロシージャを呼び出すときに、 **\@runinscaleout** パラメーターを指定する必要がなくなります。 パッケージは、Scale Out で自動的に実行されます。 

![実行モード](media/exe-mode.PNG)

パッケージが既定で Scale Out モードで実行されなくなるように、既定の実行モードを元に戻すには、 **[サーバー全体の既定の実行モード]** を **[サーバー]** に設定します。

## <a name="run-package-in-sql-server-agent-job"></a><a name="sql_agent"></a> SQL Server エージェント ジョブでパッケージを実行する
SQL Server エージェント ジョブで、ジョブの 1 つの手順として SSIS パッケージを実行することができます。 Scale Out でパッケージを実行するには、既定の実行モードを **Scale Out** に設定します。既定の実行モードを **Scale Out** に設定すると、SQL Server エージェント ジョブ内のパッケージが Scale Out モードで実行されます。

> [!NOTE]
> SQL Server エージェント ジョブをキャンセルして、Scale Out パッケージの実行を停止することはできません。 Scale Out の実行を停止するには、catalog.stop_operation ストアド プロシージャを使用するか、 **[アクティブな操作]** ペインを使用することをお勧めします。 

## <a name="next-steps"></a>次のステップ
-   [Scale Out のトラブルシューティング](troubleshooting-scale-out.md)
