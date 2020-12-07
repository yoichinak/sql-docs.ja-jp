---
description: sp_syscollector_create_collection_set (Transact-sql)
title: sp_syscollector_create_collection_set (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_set_TSQL
- sp_syscollector_create_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_create_collection_set
ms.assetid: 69e9ff0f-c409-43fc-89f6-40c3974e972c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c2f62ec06ebda9c7c22ec381f4b9b5a3011cc4f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547374"
---
# <a name="sp_syscollector_create_collection_set-transact-sql"></a>sp_syscollector_create_collection_set (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  新しいコレクションセットを作成します。 このストアドプロシージャを使用すると、データコレクションのカスタムコレクションセットを作成できます。  
  
> [!WARNING]  
>  プロキシとして構成されている Windows アカウントが、まだログインしていない非対話型または対話型ユーザーである場合、プロファイルディレクトリは存在せず、ステージングディレクトリの作成は失敗します。 したがって、ドメイン コントローラーでプロキシ アカウントを使用している場合は、プロファイル ディレクトリが確実に作成されているようにするため、少なくとも 1 回は使用されている対話型アカウントを指定する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_create_collection_set   
      [ @name = ] 'name'  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    , [ [ @schedule_uid = ] 'schedule_uid' ]  
    , [ [ @schedule_name = ] 'schedule_name' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
    , [ @collection_set_id = ] collection_set_id OUTPUT   
    , [ [ @collection_set_uid = ] 'collection_set_uid' OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` コレクションセットの名前を指定します。 *名前* は **sysname** で、空の文字列または NULL にすることはできません。  
  
 *名前* は一意である必要があります。 現在のコレクション セットの名前の一覧については、syscollector_collection_sets システム ビューにクエリを実行します。  
  
`[ @target = ] 'target'` 将来使用するために予約されています。 *名前* は **nvarchar (128)** で、既定値は NULL です。  
  
`[ @collection_mode = ] collection_mode` データを収集して格納する方法を指定します。 *collection_mode* は **smallint** であり、次のいずれかの値を持つことができます。  
  
 0-キャッシュモード。 データの収集とアップロードは別々のスケジュールに基づいています。 連続コレクションのキャッシュモードを指定します。  
  
 1-非キャッシュモード。 データの収集とアップロードは同じスケジュールに基づいて実行されます。 アドホック コレクションまたはスナップショット コレクションの非キャッシュ モードを指定します。  
  
 *Collection_mode*の既定値は0です。 *Collection_mode*が0の場合、 *schedule_uid*または*schedule_name*を指定する必要があります。  
  
`[ @days_until_expiration = ] days_until_expiration` 収集したデータを管理データウェアハウスに保存する日数を指定します。 *days_until_expiration* は **smallint** で、既定値は 730 (2 年) です。 *days_until_expiration* は、0または正の整数である必要があります。  
  
`[ @proxy_id = ] proxy_id` エージェントプロキシアカウントの一意の識別子を示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *proxy_id* は **int** で、既定値は NULL です。 指定する場合、 *proxy_name* は NULL である必要があります。 *Proxy_id*を取得するには、sysproxies システムテーブルに対してクエリを実行します。 Dc_admin 固定データベースロールには、プロキシにアクセスする権限が必要です。 詳細については、「 [Create a SQL Server エージェント Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)」を参照してください。  
  
`[ @proxy_name = ] 'proxy_name'` プロキシアカウントの名前を指定します。 *proxy_name* は **sysname** で、既定値は NULL です。 指定する場合、 *proxy_id* は NULL である必要があります。 *Proxy_name*を取得するには、sysproxies システムテーブルに対してクエリを実行します。  
  
`[ @schedule_uid = ] 'schedule_uid'` は、スケジュールを指す GUID です。 *schedule_uid* は **uniqueidentifier** で、既定値は NULL です。 指定する場合、 *schedule_name* は NULL である必要があります。 *Schedule_uid*を取得するには、sysschedules システムテーブルに対してクエリを実行します。  
  
 *Collection_mode*が0に設定されている場合、 *schedule_uid*または*schedule_name*を指定する必要があります。 *Collection_mode*が1に設定されている場合、指定した場合、 *schedule_uid*または*schedule_name*は無視されます。  
  
`[ @schedule_name = ] 'schedule_name'` スケジュールの名前を指定します。 *schedule_name* は **sysname** で、既定値は NULL です。 指定する場合、 *schedule_uid* は NULL である必要があります。 *Schedule_name*を取得するには、sysschedules システムテーブルに対してクエリを実行します。  
  
`[ @logging_level = ] logging_level` はログ記録レベルです。 *logging_level* は、次のいずれかの **値を使用** します。  
  
 0: 実行情報と [!INCLUDE[ssIS](../../includes/ssis-md.md)] 追跡するイベントを記録します。  
  
-   コレクションセットの開始/停止  
  
-   パッケージの開始/停止  
  
-   エラー情報  
  
 1 - レベル 0 の情報に加えて、以下の情報をログに記録します。  
  
-   実行の統計  
  
-   継続的に実行されているコレクションの進行状況  
  
-   からの警告イベント [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2-レベル1のログ記録と詳細なイベント情報 [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 *Logging_level*の既定値は1です。  
  
`[ @description = ] 'description'` コレクションセットの説明を設定します。 *説明* は **nvarchar (4000)** で、既定値は NULL です。  
  
`[ @collection_set_id = ] collection_set_id` コレクションセットの一意なローカル識別子を設定します。 *collection_set_id* は **int** で出力され、必須です。  
  
`[ @collection_set_uid = ] 'collection_set_uid'` コレクションセットの GUID を設定します。 *collection_set_uid* は **uniqueidentifier** で、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_syscollector_create_collection_set は、msdb システム データベースのコンテキストで実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、dc_admin (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-creating-a-collection-set-by-using-default-values"></a>A. 既定値を使用してコレクションセットを作成する  
 次の例では、必須パラメーターのみを指定してコレクション セットを作成します。 `@collection_mode` は必須ではありませんが、既定のコレクションモード (キャッシュ) では、スケジュール ID またはスケジュール名のいずれかを指定する必要があります。  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
EXECUTE dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 1',  
    @description = N'This is a test collection set that runs in non-cached mode.',  
    @collection_mode = 1,  
    @collection_set_id = @collection_set_id OUTPUT;  
GO  
```  
  
### <a name="b-creating-a-collection-set-by-using-specified-values"></a>B. 指定された値を使用してコレクションセットを作成する  
 次の例では、多くのパラメーターに値を指定してコレクションセットを作成します。  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier;  
SET @collection_set_uid = NEWID();  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 2',  
    @collection_mode = 0,  
    @days_until_expiration = 365,  
    @description = N'This is a test collection set that runs in cached mode.',  
    @logging_level = 2,  
    @schedule_name = N'CollectorSchedule_Every_30min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
```  
  
## <a name="see-also"></a>参照  
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [ジェネリック T-SQL Query コレクター型を使用するカスタム コレクション セットの作成 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
