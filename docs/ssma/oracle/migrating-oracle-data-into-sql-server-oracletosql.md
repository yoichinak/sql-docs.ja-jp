---
title: Oracle データの SQL Server への移行 (OracleToSQL) |Microsoft Docs
description: SSMA for Oracle アプリケーションを使用して、変換されたオブジェクトを同期した後に、Oracle データベースのデータを SQL Server に移行する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle Data Migration, Client-Side Migration
- Oracle Data Migration,Server-Side Migration
ms.assetid: e23c5268-41ed-4e55-9fe7-a11376202a13
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 5b22dfee8112beb7419408dfc8a3dcadf53c631d
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035165"
---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>SQL Server (OracleToSQL) に Oracle のデータの移行
変換されたオブジェクトとを正常に同期したら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、データを Oracle からに移行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!IMPORTANT]  
> 使用されているエンジンがサーバー側のデータ移行エンジンである場合は、データを移行する前に、ssma for Oracle 拡張パックと Oracle プロバイダーを SSMA を実行しているコンピューターにインストールする必要があります。 SQL Server エージェントサービスも実行されている必要があります。 拡張機能パックをインストールする方法の詳細については、「[サーバーコンポーネントのインストール」 (OracleToSQL)](./installing-ssma-components-on-sql-server-oracletosql.md)を参照してください。  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
にデータを移行する前に、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **プロジェクトの設定** ] ダイアログボックスでプロジェクトの移行オプションを確認します。  
  
-   このダイアログボックスを使用すると、移行バッチサイズ、テーブルロック、制約チェック、null 値処理、id 値の処理などのオプションを設定できます。 プロジェクトの移行設定の詳細については、「 [プロジェクトの設定 (移行)」 (OracleToSQL)](./project-settings-migration-oracletosql.md)を参照してください。  
  
-   [**プロジェクトの設定**] ダイアログボックスの**移行エンジン**を使用すると、ユーザーは2種類のデータ移行エンジンを使用して移行プロセスを実行できます。  
  
    1.  クライアント側のデータ移行エンジン  
  
    2.  サーバー側のデータ移行エンジン  
  
**クライアント側のデータ移行:**  
  
-   クライアント側でデータ移行を開始するには、[**プロジェクトの設定**] ダイアログボックスで [**クライアント側のデータ移行エンジン**] オプションを選択します。  
  
-   [ **プロジェクトの設定**] で、[ **クライアント側のデータ移行エンジン** ] オプションが設定されています。  
  
    > [!NOTE]  
    > **クライアント側のデータ移行エンジン**は ssma アプリケーション内に存在するため、拡張パックの可用性には依存しません。  
  
**サーバー側のデータ移行:**  
  
-   サーバー側のデータ移行中に、エンジンはターゲットデータベースに配置されます。 拡張機能パックを使用してインストールされます。 拡張機能パックをインストールする方法の詳細については、「 [SQL Server でのサーバーコンポーネントのインストール](installing-ssma-components-on-sql-server-oracletosql.md)」を参照してください。  
  
-   サーバー側で移行を開始するには、[**プロジェクトの設定**] ダイアログボックスで [**サーバー側のデータ移行エンジン**] オプションを選択します。  
  
## <a name="migrating-data-to-sql-server"></a>SQL Server へのデータの移行  
データの移行は、Oracle テーブルからのデータ行を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクション内のテーブルに移動する一括読み込み操作です。 各トランザクションでに読み込まれる行の数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、プロジェクトの設定で構成されます。  
  
移行メッセージを表示するには、[出力] ウィンドウが表示されていることを確認します。 それ以外の場合は、[ **表示** ] メニューの [ **出力**] を選択します。  
  
**データを移行するには**  
  
1.  次の点を確認します。  
  
    -   Oracle プロバイダーは、SSMA を実行しているコンピューターにインストールされます。  
  
    -   変換されたオブジェクトをデータベースと同期しました [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  Oracle メタデータエクスプローラーで、移行するデータを含むオブジェクトを選択します。  
  
    -   すべてのスキーマのデータを移行するには、[ **スキーマ**] の横にあるチェックボックスをオンにします。  
  
    -   データを移行するか、個々のテーブルを省略するには、まずスキーマを展開し、[ **テーブル**] を展開して、テーブルの横にあるチェックボックスをオンまたはオフにします。  
  
3.  データを移行するには、次の2つのケースが発生します。  
  
    **クライアント側のデータ移行:**  
  
    -   **クライアント側のデータ移行**を実行するには、[**プロジェクトの設定**] ダイアログボックスで [**クライアント側のデータ移行エンジン**] オプションを選択します。  
  
    **サーバー側のデータ移行:**  
  
    -   サーバー側でデータ移行を実行する前に、次のことを確認してください。  
  
        1.  SSMA for Oracle 拡張パックは、のインスタンスにインストールされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
        2.  SQL Server エージェントサービスは SQL Server のインスタンスで実行されています。  
  
    -   **サーバー側のデータ移行**を実行するには、[**プロジェクトの設定**] ダイアログボックスで [**サーバー側のデータ移行エンジン**] オプションを選択します。  
  
4.  Oracle メタデータエクスプローラーで [ **スキーマ** ] を右クリックし、[ **データの移行**] をクリックします。 また、個々のオブジェクトまたはオブジェクトのカテゴリのデータを移行することもできます。オブジェクトまたはその親フォルダーを右クリックします。[ **データの移行** ] オプションを選択します。  
  
    > [!NOTE]  
    > SSMA for Oracle 拡張パックがのインスタンスにインストールされておらず、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **サーバー側のデータ移行エンジン** が選択されている場合、ターゲットデータベースにデータを移行しているときに、次のエラーが発生します: ' ssma データ移行コンポーネントが SQL Server に見つかりませんでした。サーバー側のデータ移行は実行できません。 拡張パックが正しくインストールされているかどうかを確認してください。 [ **キャンセル** ] をクリックして、データ移行を終了します。  
  
5.  [ **Oracle への接続** ] ダイアログボックスで、接続の資格情報を入力し、[ **接続**] をクリックします。 Oracle への接続の詳細については、「 [Connect To oracle &#40;OracleToSQL](../../ssma/oracle/connect-to-oracle-oracletosql.md) 」を参照してください&#41;  
  
    ターゲットデータベースに接続するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ **SQL Server への接続** ] ダイアログボックスに接続資格情報を入力し、[ **接続**] をクリックします。 への接続の詳細につい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ては、「 [Connect to SQL Server](../sybase/connecting-to-sql-server-sybasetosql.md) 」を参照してください。  
  
    メッセージが [ **出力** ] ウィンドウに表示されます。 移行が完了すると、 **データ移行レポート** が表示されます。 データが移行されなかった場合は、エラーが含まれている行をクリックし、[ **詳細**] をクリックします。 レポートの作成が完了したら、[ **閉じる**] をクリックします。 データ移行レポートの詳細については、「[データ移行レポート (SSMA Common)](../sybase/data-migration-report-sybasetosql.md) 」を参照してください。  
  
> [!NOTE]  
> ターゲットデータベースとして SQL Express edition を使用すると、クライアント側のデータの移行のみが許可され、サーバー側のデータ移行はサポートされません。  
  
## <a name="see-also"></a>参照  
[Oracle データベースの SQL Server &#40;OracleToSQL&#41;への移行 ](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
