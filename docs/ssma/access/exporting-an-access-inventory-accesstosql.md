---
description: アクセスインベントリのエクスポート (アクセス許可 Sql)
title: アクセスインベントリのエクスポート (アクセス許可 Sql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 112452e9e6c31810dbf26d9aa1e7b36959c192d5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488335"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>アクセスインベントリのエクスポート (アクセス許可 Sql)
複数の Access データベースがあり、どのデータベースに移行するかがわからない場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、プロジェクト内のすべての access データベースのインベントリをエクスポートできます。 次に、インベントリメタデータを確認してクエリを実行し、移行するデータベースとデータベース内のオブジェクトを確認できます。 このインベントリを使用すると、次のような質問に対する回答をすばやく見つけることができます。  
  
-   最大のデータベースは何ですか。  
  
-   ほとんどのデータベースを所有しているのはだれですか。  
  
-   同じテーブルを含むデータベース  
  
-   過去6か月間、どのデータベースが変更されていませんか?  
  
-   プライベート情報が含まれているデータベース  
  
これらの質問に答えるために使用されるクエリの例については、このトピックの最後を参照してください。  
  
## <a name="exported-metadata"></a>エクスポートされたメタデータ  
SSMA は、Access データベース、テーブル、列、インデックス、外部キー、クエリ、レポート、フォーム、マクロ、およびモジュールに関するメタデータをエクスポートします。 これらの項目の各カテゴリに関するメタデータは、別のテーブルにエクスポートされます。 これらのテーブルのスキーマについては、「 [Access Inventory schema](access-inventory-schemas-accesstosql.md)」を参照してください。  
  
## <a name="exporting-inventory-data"></a>インベントリデータのエクスポート  
アクセスインベントリをエクスポートするには、まず SSMA プロジェクトを開くか作成し、次に分析する Access データベースを追加する必要があります。 SSMA プロジェクトにデータベースを追加した後、これらのデータベースに関するメタデータを指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースとスキーマにエクスポートします。 SSMA では、必要に応じて、メタデータを格納するテーブルを作成します。 SSMA は、Access データベースに関するメタデータをデータベースに追加し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!NOTE]  
> Access データベースは、複数のファイルに分割できます。これには、クエリ、フォーム、レポート、マクロ、モジュール、およびショートカットを含むテーブルとフロントエンドデータベースを格納するバックエンドデータベースが含まれます。 分割されたデータベースをに移行する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、フロントエンドデータベースを SSMA に追加します。  
  
次の手順では、プロジェクトの作成、プロジェクトへのデータベースの追加、インベントリデータの接続、およびエクスポートを行う方法について説明し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**プロジェクトを作成するには**  
  
1.  SSMA を開いてアクセスします。  
  
2.  **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  [ **名前** ] ボックスに、プロジェクトの名前を入力します。  
  
4.  [ **場所** ] ボックスで、プロジェクトのフォルダーを入力または選択します。  
  
5.  [ **移行** 先] コンボボックスで、移行するターゲットバージョンを選択し、[ **OK**] をクリックします。  
  
プロジェクトの作成の詳細については、「 [プロジェクトの作成と管理](creating-and-managing-projects-accesstosql.md)」を参照してください。  
  
**データベースを検索して追加するには**  
  
1.  [ **ファイル** ] メニューの [ **データベースの検索**] をクリックします。  
  
2.  [データベースの検索] ウィザードで、検索するドライブ、ファイルパス、または UNC パスを入力します。 または、[ **参照** ] をクリックして、ドライブまたはネットワークフォルダーを選択します。  
  
3.  [ **追加** ] をクリックして、リストボックスに場所を追加します。  
  
    前の2つの手順を繰り返して、別の検索場所を追加します。  
  
4.  必要に応じて、検索条件を追加して、返されるデータベースの一覧を絞り込むことができます。  
  
    > [!IMPORTANT]  
    > [ **ファイル名] テキストボックスの全体または一部** がワイルドカード文字をサポートしていません。  
  
5.  **[スキャン]** をクリックします。  
  
    スキャンページが表示されます。 これにより、検出されたデータベースと検索の進行状況が表示されます。 検索を停止するには、[ **停止**] をクリックします。  
  
6.  [ファイルの選択] ページで、プロジェクトに追加する各データベースを選択します。  
  
    すべてのデータベースを選択または選択解除するには、一覧の上部にある **[すべて選択]** ボタンと [ **すべてクリア** ] ボタンを使用します。 また、CTRL キーを押しながら複数の行を選択したり、SHIFT キーを押しながら行の範囲を選択したりすることもできます。  
  
7.  **[次へ]** をクリックします。  
  
8.  [確認] ページで、[ **完了**] をクリックします。  
  
プロジェクトへのデータベースの追加の詳細については、「 [Access データベースファイルの追加と削除](adding-and-removing-access-database-files-accesstosql.md)」を参照してください。  
  
**SQL Server に接続するには**  
  
1.  [ **ファイル** ] メニューの [ **SQL Server に接続**] を選択します。  
  
2.  [接続] ダイアログボックスで、のインスタンスの名前を入力または選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
    -   ローカルコンピューター上の既定のインスタンスに接続している場合は、 **localhost** またはドット (**.**) を入力できます。  
  
    -   別のコンピューター上の既定のインスタンスに接続している場合は、コンピューターの名前を入力します。  
  
    -   名前付きインスタンスに接続する場合は、コンピューター名、円記号、およびインスタンス名を入力します。 例: My\ myinstance。  
  
3.  [ **データベース** ] ボックスに、エクスポートされたメタデータのターゲットデータベースの名前を入力します。  
  
4.  のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が既定以外のポートで接続を受け入れるように構成されている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ **サーバーポート** ] ボックスに接続に使用するポート番号を入力します。 の既定のインスタンスの場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、既定のポート番号は1433です。 名前付きインスタンスの場合、SSMA は Browser サービスからポート番号の取得を試み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
5.  [ **認証** ] ドロップダウンメニューで、接続に使用する認証の種類を選択します。 現在の Windows アカウントを使用するには、[ **Windows 認証**] を選択します。 ログインを使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **SQL Server 認証**] を選択し、ユーザー名とパスワードを入力します。  
  
への接続の詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、「 [SQL Server への接続 &#40;](../../ssma/access/connecting-to-sql-server-accesstosql.md)の使用」&#41;を参照してください。  
  
**インベントリ情報をエクスポートするには**  
  
1.  Access Metadata Explorer で、[ **アクセス-メタベース**] を展開します。  
  
2.  [ **データベース**] の横にあるチェックボックスをオンにします。  
  
    個々のデータベースまたはデータベースオブジェクトを省略するには、[ **データベース** ] フォルダーを展開し、データベースまたはデータベースオブジェクトの横にあるチェックボックスをオフにします。  
  
3.  [ **データベース** ] を右クリックし、[ **スキーマのエクスポート**] を選択します。  
  
4.  [ **エクスポートするスキーマの選択** ] ダイアログボックスで、エクスポートされたメタデータのターゲットスキーマを選択し、[ **OK**] をクリックします。  
  
メタデータをエクスポートするたびに、SSMA によってデータがインベントリに追加されます。 インベントリ内の既存のデータは更新または削除されません。  
  
## <a name="querying-the-exported-metadata"></a>エクスポートされたメタデータのクエリ  
Access データベースに関するメタデータをエクスポートした後、メタデータに対してクエリを実行できます。 次の手順では、のクエリエディターウィンドウを使用してクエリを実行する方法について説明し [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。  
  
**メタデータを照会するには**  
  
1.  [ **スタート** ] ボタンをクリックし、[ **すべてのプログラム**] をポイントします。次に、[ **microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005** ] または [microsoft ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008** または **microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012**] をポイントし、[ **SQL Server Management Studio**] をクリックします。  
  
2.  [ **サーバーへの接続** ] ダイアログボックスで、設定を確認し、[ **接続**] をクリックします。  
  
3.  [Management Studio] ツールバーの [ **新しいクエリ** ] をクリックして、クエリエディターを開きます。  
  
4.  クエリエディターウィンドウで、クエリを入力します。 次のセクションでは、いくつかの例を示します。  
  
5.  F5 キーを押してクエリを実行します。  
  
## <a name="query-examples"></a>クエリの例  
次のクエリのいずれかを実行する前に、 *database_name* クエリを使用して、エクスポートされたメタデータを含むデータベースに対してクエリが実行されていることを確認する必要があります。 たとえば、MyAccessMetadata という名前のデータベースにメタデータをエクスポートした場合、コードの先頭に次のコードを追加し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
```  
USE MyAccessMetadata;  
GO  
```  
次の例では、すべて **dbo** スキーマを使用します。 メタデータを別のスキーマにエクスポートした場合は、これらのクエリを実行するときにスキーマを変更してください。  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>これらのデータベースにはどのようなテーブルと列が含まれていますか。  
次のクエリは、列、テーブル、およびデータベースのメタデータを含むテーブルを結合し、列名で並べ替えられたすべてのデータベース、テーブル、および列の名前を返します。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>最大のデータベースは何ですか。  
次のクエリは、各 Access データベースのデータベース名、ファイルサイズ、およびテーブルの数を、ファイルサイズで並べ替えて返します。  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>ほとんどのデータベースの所有者はだれですか。  
次のクエリは、所有者別に並べ替えられた、各 Access データベースのデータベース名と所有者を返します。  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>同じテーブルを含むデータベース  
次のクエリでは、サブクエリを使用して、テーブルの一覧に2回以上表示されているすべてのテーブル名を検索し、このテーブルの一覧を使用してデータベース名を取得します。 結果はデータベース名として返され、テーブル名の後にテーブル名で並べ替えられます。  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>過去6か月間、どのデータベースが変更されなかったか。  
次のクエリでは、現在の日付を取得し、6か月前の月の値を取得してから、変更日が6か月前のデータベースの一覧を返します。  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>プライベート情報が含まれているデータベース  
Access データベースには、機密情報や個人情報が含まれている場合があります。 これらのデータベースをに移動して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、セキュリティ機能を利用することもできます。 機密データを含む列に特定の名前が付いていることがわかっている場合や、特定の文字が含まれている場合は、クエリを使用してその情報を含むすべての列を検索できます。 たとえば、"salary" という文字列を含むすべての列を検索できます。  次に、クエリによって、データベース名、テーブル名、および列名が返されます。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
列名がわからない場合は、すべての列を返すクエリを記述できます。 これを行うには、前のクエリから WHERE 句を削除します。  
  
## <a name="see-also"></a>関連項目  
[Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)  
  
