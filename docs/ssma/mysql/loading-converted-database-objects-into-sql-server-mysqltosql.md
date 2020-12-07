---
description: SQL Server への変換されたデータベース オブジェクトの読み込み (MySQLToSQL)
title: 変換されたデータベースオブジェクトを SQL Server に読み込んでいます (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 87960d05db8a12ebd7a8751f46c90a256ce73313
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463396"
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>SQL Server への変換されたデータベース オブジェクトの読み込み (MySQLToSQL)
MySQL データベースをまたは SQL Azure に変換した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、結果として得られるデータベースオブジェクトをまたは SQL Azure に読み込むことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 SSMA を使用してオブジェクトを作成するか、オブジェクトのスクリプトを作成して自分でスクリプトを実行することができます。 また、SSMA では、または Azure SQL Database の実際の内容でターゲットメタデータを更新することもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同期とスクリプトの選択  
変換されたデータベースオブジェクトを変更せずにまたは SQL Azure に読み込む場合は、SSMA を使用し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] てデータベースオブジェクトを直接作成または再作成することができます。 この方法は短時間で簡単ですが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトまたは SQL Azure オブジェクトを定義する transact-sql コードをカスタマイズすることはできません。  
  
オブジェクトの作成に使用される Transact-sql を変更する場合、またはオブジェクトの作成をより細かく制御する場合は、SSMA を使用してスクリプトを作成します。 これらのスクリプトを変更し、各オブジェクトを個別に作成し、SQL Server エージェントを使用してこれらのオブジェクトの作成をスケジュールすることもできます。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA を使用してオブジェクトを SQL Server と同期させる  
SSMA を使用して SQL Server オブジェクトまたは Azure SQL Database オブジェクトを作成するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、または SQL Azure メタデータエクスプローラーでオブジェクトを選択し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 次の手順に示すように、または SQL Azure を使用してオブジェクトを同期します。 既定では、オブジェクトが既にまたは SQL Azure に存在する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma メタデータの一部のローカルな変更や、それらのオブジェクトの定義に対する更新がある場合、SSMA はまたは SQL Azure のオブジェクト定義を変更し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定の動作を変更するには、 **プロジェクトの設定**を編集します。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MySQL データベースから変換されなかった既存のオブジェクトまたは Azure SQL Database オブジェクトを選択できます。 ただし、これらのオブジェクトは SSMA によって再作成または変更されることはありません。  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>SQL Server または SQL Azure とオブジェクトを同期するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータエクスプローラーで、上部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [SQL Azure] ノードを展開し、[**データベース**] を展開します。  
  
2.  処理するオブジェクトを選択してください:  
  
    -   データベース全体を同期するには、データベース名の横にあるチェックボックスをオンにします。  
  
    -   個々のオブジェクトまたはオブジェクトのカテゴリを同期または除外するには、オブジェクトまたはフォルダーの横にあるチェックボックスをオンまたはオフにします。  
  
3.  SQL Server または SQL Azure メタデータエクスプローラーで処理するオブジェクトを選択したら、[ **データベース**] を右クリックし、[ **データベースとの同期**] をクリックします。  
  
    オブジェクトまたはオブジェクトのカテゴリを右クリックし、[ **データベースとの同期**] をクリックして、個々のオブジェクトまたはオブジェクトのカテゴリを同期させることもできます。  
  
    その後、SSMA の [ **データベースとの同期** ] ダイアログボックスが表示され、2つのアイテムのグループが表示されます。 左側の SSMA は、ツリーで表される選択されたデータベースオブジェクトを示しています。 右側には、SSMA メタデータ内の同じオブジェクトを表すツリーが表示されます。 ツリーを展開するには、右または左の [+] ボタンをクリックします。 同期の方向は、2つのツリーの間に配置されたアクション列に表示されます。  
  
    アクションの署名には、次の3つの状態があります。  
  
    -   左矢印は、メタデータの内容がデータベースに保存されることを意味します (既定値)。  
  
    -   右矢印は、データベースの内容が SSMA メタデータを上書きすることを意味します。  
  
    -   クロス署名は、何も実行されないことを意味します。  
  
    -   操作の署名をクリックして、状態を変更します。 実際の同期は、[**データベースとの同期**] ダイアログの [ **OK** ] ボタンをクリックしたときに実行されます。  
  
## <a name="scripting-objects"></a>スクリプトオブジェクト  
変換された [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースオブジェクトの定義を保存する、またはオブジェクトの定義を変更してスクリプトを実行するには、変換されたデータベースオブジェクトの定義をスクリプトに保存し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
**オブジェクトをスクリプトとして保存するには**  
  
1.  スクリプトに保存するオブジェクトを選択したら、[ **データベース**] を右クリックし、[ **スクリプトとして保存**] をクリックします。  
  
    オブジェクトまたはその親フォルダーを右クリックし、[ **スクリプトとして保存**] をクリックして、個々のオブジェクトまたはオブジェクトのカテゴリをスクリプト化することもできます。  
  
2.  [名前を **付けて保存** ] ダイアログボックスで、スクリプトを保存するフォルダーに移動し、[ **ファイル名** ] ボックスにファイル名を入力すると、 [!INCLUDE[clickOK](../../includes/clickok-md.md)] ssma によって .sql ファイル名拡張子が追加されます。  
  
### <a name="modifying-scripts"></a>スクリプトの変更  
SQL Server または SQL Azure オブジェクトの定義をスクリプトとして保存した後、SQL Server Management Studio を使用してスクリプトを変更できます。  
  
**スクリプトを変更するには**  
  
1.  [Management Studio **ファイル** ] メニューの [ **開く**] をポイントし、[ **ファイル**] をクリックします。  
  
2.  [開く] ダイアログボックスで、スクリプトファイルを探して選択し、[ **OK**] をクリックします。  
  
3.  クエリエディターを使用して、スクリプトファイルを編集します。クエリエディターの詳細については、SQL Server オンラインブックの「エディターの便利なコマンドと機能」を参照してください。  
  
4.  スクリプトを保存するには、[ファイル] メニューの [ **保存**] をクリックします。  
  
### <a name="running-scripts"></a>スクリプトの実行  
SQL Server Management Studio では、スクリプトまたは個別のステートメントを実行できます。  
  
**スクリプトを実行するには**  
  
1.  [SQL Server Management Studio **ファイル** ] メニューの [ **開く** ] をポイントし、[ **ファイル**] をクリックします。  
  
2.  [開く] ダイアログボックスで、スクリプトファイルを探して選択し、[ **OK**] をクリックします。  
  
3.  スクリプト全体を実行するには、 **F5** キーを押します。  
  
4.  一連のステートメントを実行するには、クエリエディターウィンドウでステートメントを選択し、 **F5** キーを押します。  
  
5.  クエリエディターを使用してスクリプトを実行する方法の詳細については、「SQL Server オンラインブック」の「Transact-sql クエリの SQL Server Management Studio」を参照してください。  
  
6.  また、 **sqlcmd** ユーティリティを使用してコマンドラインからスクリプトを実行したり、SQL Server エージェントからスクリプトを実行したりすることもできます。 **Sqlcmd**の詳細については、SQL Server オンラインブックの「sqlcmd ユーティリティ」を参照してください。 SQL Server エージェントの詳細については、SQL Server オンラインブックの「管理タスクの自動化 (SQL Server エージェント)」を参照してください。  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server でのオブジェクトのセキュリティ保護  
変換されたデータベースオブジェクトを SQL Server に読み込むと、これらのオブジェクトに対する権限を許可したり拒否したりできます。 SQL Server にデータを移行する前に、これを行うことをお勧めします。 SQL Server でオブジェクトをセキュリティで保護する方法の詳細については、「SQL Server オンラインブック」の「データベースとデータベースアプリケーションのセキュリティに関する考慮事項」を参照してください。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次のステップでは、 [MySQL データを SQL Server Azure SQL Database &#40;MySQLToSQL に移行](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)してい&#41;  
  
## <a name="see-also"></a>参照  
[MySQL データベースを SQL Server Azure SQL Database &#40;MySQLToSql&#41;に移行する ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
