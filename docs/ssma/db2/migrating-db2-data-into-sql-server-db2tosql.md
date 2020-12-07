---
title: DB2 データの SQL Server への移行 (DB2ToSQL) |Microsoft Docs
description: 変換されたオブジェクトを同期した後、DB2 データベースから SQL Server または Azure SQL Database にデータを移行する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2f3ca5b9f222e52b7913d5688b6e8c6adfbd526d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869730"
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>DB2 データの SQL Server への移行 (DB2ToSQL)
変換されたオブジェクトとを正常に同期したら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、DB2 からにデータを移行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!IMPORTANT]  
> 使用されているエンジンがサーバー側のデータ移行エンジンである場合、データを移行する前に、ssma for DB2 拡張パックと、SSMA を実行しているコンピューターに DB2 プロバイダーをインストールする必要があります。 SQL Server エージェントサービスも実行されている必要があります。 拡張機能パックをインストールする方法の詳細については、「 [SQL Server での SSMA コンポーネントのインストール](./installing-ssma-components-on-sql-server-db2tosql.md)」を参照してください。  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
にデータを移行する前に、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **プロジェクトの設定** ] ダイアログボックスでプロジェクトの移行オプションを確認します。  
  
-   このダイアログボックスを使用すると、移行バッチサイズ、テーブルロック、制約チェック、null 値処理、id 値の処理などのオプションを設定できます。 プロジェクトの移行設定の詳細については、「 [プロジェクトの設定 (移行)](./project-settings-migration-db2tosql.md)」を参照してください。  
  
-   [**プロジェクトの設定**] ダイアログボックスの **移行エンジン** を使用すると、ユーザーは2種類のデータ移行エンジンを使用して移行プロセスを実行できます。  
  
    1.  クライアント側のデータ移行エンジン  
  
    2.  サーバー側のデータ移行エンジン  
  
**クライアント側のデータ移行:**  
  
-   クライアント側でデータ移行を開始するには、[**プロジェクトの設定**] ダイアログボックスで [**クライアント側のデータ移行エンジン**] オプションを選択します。  
  
-   [ **プロジェクトの設定**] で、[ **クライアント側のデータ移行エンジン** ] オプションが設定されています。  
  
    > [!NOTE]  
    > **クライアント側のデータ移行エンジン** は ssma アプリケーション内に存在するため、拡張パックの可用性には依存しません。  
  
**サーバー側のデータ移行:**  
  
-   サーバー側のデータ移行中に、エンジンはターゲットデータベースに配置されます。 拡張機能パックを使用してインストールされます。 拡張機能パックをインストールする方法の詳細については、「 [SQL Server での SSMA コンポーネントのインストール](./installing-ssma-components-on-sql-server-db2tosql.md)」を参照してください。  
  
-   サーバー側で移行を開始するには、[**プロジェクトの設定**] ダイアログボックスで [**サーバー側のデータ移行エンジン**] オプションを選択します。  
  
## <a name="migrating-data-to-sql-server"></a>SQL Server へのデータの移行  
データの移行は、DB2 テーブルからのデータ行を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクション内のテーブルに移動する一括読み込み操作です。 各トランザクションでに読み込まれる行の数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、プロジェクトの設定で構成されます。  
  
移行メッセージを表示するには、[出力] ウィンドウが表示されていることを確認します。 それ以外の場合は、[ **表示** ] メニューの [ **出力**] を選択します。  
  
**データを移行するには**  
  
1.  次の点を確認します。  
  
    -   DB2 プロバイダーは、SSMA を実行しているコンピューターにインストールされます。  
  
    -   変換されたオブジェクトをデータベースと同期しました [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  DB2 メタデータエクスプローラーで、移行するデータを含むオブジェクトを選択します。  
  
    -   すべてのスキーマのデータを移行するには、[ **スキーマ**] の横にあるチェックボックスをオンにします。  
  
    -   データを移行するか、個々のテーブルを省略するには、まずスキーマを展開し、[ **テーブル**] を展開して、テーブルの横にあるチェックボックスをオンまたはオフにします。  
  
3.  データを移行するには、次の2つのケースが発生します。  
  
    **クライアント側のデータ移行:**  
  
    -   **クライアント側のデータ移行** を実行するには、[**プロジェクトの設定**] ダイアログボックスで [**クライアント側のデータ移行エンジン**] オプションを選択します。  
  
    **サーバー側のデータ移行:**  
  
    -   サーバー側でデータ移行を実行する前に、次のことを確認してください。  
  
        1.  SSMA for DB2 拡張パックは、のインスタンスにインストールされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
        2.  SQL Server エージェントサービスは SQL Server のインスタンスで実行されています。  
  
    -   **サーバー側のデータ移行** を実行するには、[**プロジェクトの設定**] ダイアログボックスで [**サーバー側のデータ移行エンジン**] オプションを選択します。  
  
4.  DB2 メタデータエクスプローラーで [ **スキーマ** ] を右クリックし、[ **データの移行**] をクリックします。 また、個々のオブジェクトまたはオブジェクトのカテゴリのデータを移行することもできます。オブジェクトまたはその親フォルダーを右クリックします。[ **データの移行** ] オプションを選択します。  
  
    > [!NOTE]  
    > SSMA for DB2 拡張パックがのインスタンスにインストールされておらず、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **サーバー側のデータ移行エンジン** が選択されている場合、ターゲットデータベースにデータを移行しているときに、次のエラーが発生します: ' ssma データ移行コンポーネントが SQL Server に見つかりませんでした。サーバー側のデータ移行は実行できません。 拡張パックが正しくインストールされているかどうかを確認してください。 [ **キャンセル** ] をクリックして、データ移行を終了します。  
  
5.  [ **DB2 への接続** ] ダイアログボックスで、接続の資格情報を入力し、[ **接続**] をクリックします。 DB2 への接続の詳細については、「 [Db2 データベースへの接続 &#40;DB2ToSQL](../../ssma/db2/connecting-to-db2-database-db2tosql.md) 」を参照してください&#41;  
  
    ターゲットデータベースに接続するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ **SQL Server への接続** ] ダイアログボックスに接続資格情報を入力し、[ **接続**] をクリックします。 への接続の詳細につい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ては、「 [SQL Server への接続](./connecting-to-sql-server-db2tosql.md)」を参照してください。  
  
    メッセージが [ **出力** ] ウィンドウに表示されます。 移行が完了すると、 **データ移行レポート** が表示されます。 データが移行されなかった場合は、エラーが含まれている行をクリックし、[ **詳細**] をクリックします。 レポートの作成が完了したら、[ **閉じる**] をクリックします。 データ移行レポートの詳細については、「[データ移行レポート (SSMA Common)](../sybase/data-migration-report-sybasetosql.md) 」を参照してください。  
  
> [!NOTE]  
> ターゲットデータベースとして SQL Express edition を使用すると、クライアント側のデータの移行のみが許可され、サーバー側のデータ移行はサポートされません。  
  
## <a name="see-also"></a>参照  
[DB2 データの SQL Server &#40;DB2ToSQL&#41;への移行 ](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
