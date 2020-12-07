---
description: MySQL データの SQL Server Azure SQL Database への移行 (MySQLToSQL)
title: MySQL データの SQL Server Azure SQL Database への移行 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 16b6c68c520291b0f9ae6613940832c0fa77af68
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988168"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-database-mysqltosql"></a>MySQL データの SQL Server Azure SQL Database への移行 (MySQLToSQL)
変換されたオブジェクトをまたは SQL Azure に正常に同期した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、MySQL からまたは SQL Azure にデータを移行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!IMPORTANT]  
> 使用されているエンジンがサーバー側のデータ移行エンジンである場合、データを移行する前に、ssma を実行しているコンピューターに SSMA for MySQL Extension Pack と MySQL プロバイダーをインストールする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントサービスも実行されている必要があります。 拡張機能パックをインストールする方法の詳細については、「 [SQL Server での SSMA コンポーネントのインストール (MySQL から SQL)](./installing-ssma-components-on-sql-server-mysqltosql.md) 」を参照してください。  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
または SQL Azure にデータを移行する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [プロジェクトの **設定** ] ダイアログボックスでプロジェクトの移行オプションを確認してください。  
  
-   このダイアログボックスを使用すると、移行バッチサイズ、テーブルロック、制約チェック、null 値処理、id 値処理などのオプションを設定できます。 プロジェクトの移行設定の詳細については、「 [プロジェクトの設定 (移行)](./project-settings-migration-mysqltosql.md)」を参照してください。  
  
    **拡張データ移行設定**の詳細については、「[データ移行の設定](data-migration-settings-mysqltosql.md)」を参照してください。  
  
-   [**プロジェクトの設定**] ダイアログボックスの**移行エンジン**を使用すると、ユーザーは2種類のデータ移行エンジンを使用して移行プロセスを実行できます。  
  
    1.  クライアント側のデータ移行エンジン  
  
    2.  サーバー側のデータ移行エンジン  
  
**クライアント側のデータ移行:**  
  
-   クライアント側でデータ移行を開始するには、[**プロジェクトの設定**] ダイアログボックスで [**クライアント側のデータ移行エンジン**] オプションを選択します。  
  
-   [ **プロジェクトの設定**] で、[ **クライアント側のデータ移行エンジン** ] オプションが設定されています。  
  
    > [!NOTE]  
    > **クライアント側のデータ移行エンジン**は ssma アプリケーション内に存在するため、拡張パックの可用性には依存しません。  
  
**サーバー側のデータ移行:**  
  
-   サーバー側のデータ移行中に、エンジンはターゲットデータベースに配置されます。 拡張機能パックを使用してインストールされます。 拡張機能パックをインストールする方法の詳細については、「 [SQL Server での SSMA コンポーネントのインストール (MySQL から SQL)](./installing-ssma-components-on-sql-server-mysqltosql.md) 」を参照してください。  
  
-   サーバー側で移行を開始するには、[**プロジェクトの設定**] ダイアログボックスで [**サーバー側のデータ移行エンジン**] オプションを選択します。  
  
> [!IMPORTANT]  
> **クライアント側のデータ移行** オプションは、SQL Azure に対してのみ使用できます。  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>SQL Server または SQL Azure へのデータの移行  
データの移行は、データの行を MySQL テーブルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはトランザクション内の SQL Azure テーブルに移動する一括読み込み操作です。 各トランザクションでに読み込まれる行の数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、プロジェクトの設定で構成されます。  
  
移行メッセージを表示するには、[出力] ウィンドウが表示されていることを確認します。 それ以外の場合は、[ **表示** ] メニューの [ **出力**] を選択します。  
  
**データを移行するには**  
  
1.  次の点を確認します。  
  
    -   MySQL プロバイダーは、SSMA を実行しているコンピューターにインストールされます。  
  
    -   変換されたオブジェクトをターゲットデータベース (SQL Server/SQL Azure) と同期しました。  
  
2.  MySQL メタデータエクスプローラーで、移行するデータを含むオブジェクトを選択します。  
  
    -   すべてのスキーマのデータを移行するには、[ **スキーマ**] の横にあるチェックボックスをオンにします。  
  
    -   データを移行するか、個々のテーブルを省略するには、まずスキーマを展開し、[ **テーブル**] を展開して、テーブルの横にあるチェックボックスをオンまたはオフにします。  
  
3.  データを移行するには、次の2つのケースが発生します。  
  
    **クライアント側のデータ移行:**  
  
    -   **クライアント側のデータ移行**を実行するには、[**プロジェクトの設定**] ダイアログボックスで [**クライアント側のデータ移行エンジン**] オプションを選択します。  
  
    **サーバー側のデータ移行:**  
  
    -   サーバー側でデータ移行を実行する前に、次のことを確認してください。  
  
        1.  SSMA for MySQL Extension Pack は SQL Server のインスタンスにインストールされます。  
  
        2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントサービスは、のインスタンスで実行されて SQL Server  
  
    -   **サーバー側のデータ移行**を実行するには、[**プロジェクトの設定**] ダイアログボックスで [**サーバー側のデータ移行エンジン**] オプションを選択します。  
  
4.  MySQL メタデータエクスプローラーで [ **スキーマ** ] を右クリックし、[ **データの移行**] をクリックします。 また、個々のオブジェクトまたはオブジェクトのカテゴリのデータを移行することもできます。オブジェクトまたはその親フォルダーを右クリックします。[ **データの移行** ] オプションを選択します。  
  
    > [!NOTE]  
    > SSMA for MySQL 拡張パックが SQL Server のインスタンスにインストールされておらず、 **サーバー側のデータ移行エンジン** が選択されている場合、ターゲットデータベースにデータを移行しているときに、次のエラーが発生します。 "Ssma データ移行コンポーネントが SQL Server に見つかりませんでした。サーバー側のデータ移行は実行できません。 拡張パックが正しくインストールされているかどうかを確認してください。 [ **キャンセル** ] をクリックして、データ移行を終了します。  
  
5.  [ **MySQL への接続** ] ダイアログボックスで、接続の資格情報を入力し、[ **接続**] をクリックします。 MySQL への接続の詳細については、「 [Connect To mysql &#40;MySQLToSQL](../../ssma/mysql/connect-to-mysql-mysqltosql.md) 」を参照してください&#41;  
  
    ターゲットデータベースが SQL Server 場合は、[ **SQL Server への接続** ] ダイアログボックスで接続資格情報を入力し、[ **接続**] をクリックします。 SQL Server に接続する方法の詳細については、「 [Connect to SQL Server](../sybase/connecting-to-sql-server-sybasetosql.md) 」を参照してください。  
  
    ターゲットデータベースが SQL Azure 場合は、[ **SQL Azure への接続** ] ダイアログボックスで接続資格情報を入力し、[ **接続**] をクリックします。 SQL Azure に接続する方法の詳細については、「 [Connect to Azure SQL Database &#40;MySQLToSQL](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md) 」を参照してください&#41;  
  
    メッセージが [ **出力** ] ウィンドウに表示されます。 移行が完了すると、 **データ移行レポート** が表示されます。 データが移行されなかった場合は、エラーが含まれている行をクリックし、[ **詳細**] をクリックします。 レポートの作成が完了したら、[ **閉じる**] をクリックします。 データ移行レポートの詳細については、「[データ移行レポート (SSMA Common)](../sybase/data-migration-report-sybasetosql.md) 」を参照してください。  
  
> [!NOTE]  
> ターゲットデータベースとして SQL Express edition を使用すると、クライアント側のデータの移行のみが許可され、サーバー側のデータ移行はサポートされません。  
  
## <a name="see-also"></a>参照  
[MySQL データベースを SQL Server Azure SQL Database &#40;MySQLToSql&#41;に移行する ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
