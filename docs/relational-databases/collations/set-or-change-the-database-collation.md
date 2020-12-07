---
description: データベースの照合順序の設定または変更
title: データベースの照合順序の設定または変更 | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9ea1926c2e54135277dd486976dda7ebe4ae6086
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907385"
---
# <a name="set-or-change-the-database-collation"></a>データベースの照合順序の設定または変更
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、データベースの照合順序を設定および変更する方法を説明します。 照合順序を指定しない場合、サーバーの照合順序が使用されます。  
  
> [!IMPORTANT]
> Azure SQL Database に対する `ALTER DATABASE COLLATE` ステートメントはサポートされていません。

 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
     [Security](#Security)  
  
-   **データベースの照合順序を設定または変更する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   Windows Unicode 専用の照合順序は、COLLATE 句で、列レベルと式レベルのデータの **nchar** 、 **nvarchar** 、 **ntext** の各データ型に対して照合順序を適用する場合にのみ使用できます。 データベースまたはサーバー インスタンスの照合順序を変更するために、COLLATE 句で使用することはできません。  
  
-   指定した照合順序、または参照先のオブジェクトで使用される照合順序で、Windows でサポートされていないコード ページが使用されていると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] でエラーが表示されます。  

-   [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] でデータベースが作成された後は、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して照合順序を変更することはできません。 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用することによってのみ変更できます。
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
  
サポートされる照合順序名は、「 [Windows 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) 」と「 [SQL Server 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)」で確認できます。または、 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) システム関数を使用できます。  
  
データベースの照合順序を変更すると、次の変更が行われます。  
  
-   システム テーブル内の **char** 型、 **varchar** 型、 **text** 型、 **nchar** 型、 **nvarchar** 型、または **ntext** 型の列はすべて、新しい照合順序に変更されます。  
  
-   ストアド プロシージャおよびユーザー定義関数で使用されている **char** 、 **varchar** 、 **text** 、 **nchar** 、 **nvarchar** 、または **ntext** の既存のパラメーターおよびスカラー値の戻り値はすべて、新しい照合順序に変更されます。  
  
-   **char** 、 **varchar** 、 **text** 、 **nchar** 、 **nvarchar** 、または **ntext** のシステム データ型およびこれらを基にしたユーザー定義データ型はすべて、新しい既定の照合順序に変更されます。  
  
ユーザー データベースに作成される新しいオブジェクトの照合順序は、[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) ステートメントの `COLLATE` 句を使用して変更できます。 このステートメントを実行しても、既存のユーザー定義テーブルの列の照合順序は **変更されません** 。 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) の `COLLATE` 句で変更することができます。  

> [!IMPORTANT]
> データベースまたは個々の列の照合順序を変更しても、既存のテーブルに既に格納されている基になるデータは **変更されません** 。 アプリケーションが異なる照合順序間でデータの変換と比較を明示的に処理する場合を除き、データベース内の既存のデータを新しい照合順序に移行することをお勧めします。 これにより、アプリケーションによってデータが誤って変更され、正しくない結果が発生したり知らない間にデータが失われたりするリスクが排除されます。   

データベースの照合順序を変更すると、新しいテーブルだけが既定で新しいデータベースの照合順序を継承します。 既存のデータを新しい照合順序に変換するには、いくつかの選択肢があります。
-  適切な場所でデータを変換する。 既存のテーブル内の列の照合順序を変換する方法については、「[列の照合順序の設定または変更](../../relational-databases/collations/set-or-change-the-column-collation.md)」を参照してください。 この操作は簡単に実装できますが、大きなテーブルやビジー状態のアプリケーションで障害となっている問題になる可能性があります。 `MyString` 列から新しい照合順序へのインプレース変換については、次の例を参照してください。

   ```sql
   ALTER TABLE dbo.MyTable
   ALTER COLUMN MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8;
   ```

-  新しい照合順序を使用する新しいテーブルにデータをコピーし、同じデータベース内の元のテーブルを置換します。 現在のデータベースに、データベースの照合順序を継承する新しいテーブルを作成し、古いテーブルと新しいテーブルの間でデータをコピーしたら、元のテーブルを削除して、新しいテーブルの名前を元のテーブルの名前に変更します。 これは、インプレース変換の操作よりも高速ですが、外部キー制約、主キー制約、トリガーなどの依存関係を含む複雑なスキーマを処理する場合には困難となる場合があります。 また、データが引き続きアプリケーションによって変更される場合は、最終的なカットオフの前に、元のものと新しいテーブルの間で最終的なデータ同期も必要になります。 `MyString` 列から新しい照合順序への "コピーと変換" による変換については、次の例を参照してください。

   ```sql
   CREATE TABLE dbo.MyTable2 (MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8); 
   
   INSERT INTO dbo.MyTable2 
   SELECT * FROM dbo.MyTable; 
   
   DROP TABLE dbo.MyTable; 
   
   EXEC sp_rename 'dbo.MyTable2', 'dbo.MyTable’;
   ```

-  新しい照合順序を使用する新しいデータベースにデータをコピーし、元のデータベースを置き換えます。 新しい照合順序を使用して新しいデータベースを作成し、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] や [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のインポート/エクスポート ウィザードのようなツールを使用して、元のデータベースのデータを転送します。 これは、複雑なスキーマのためのより簡単な方法です。 また、データが引き続きアプリケーションによって変更される場合は、最終的なカットオフの前に、元のものと新しいデータベースの間で最終的なデータ同期も必要になります。
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 新しいデータベースを作成するには、 **master** データベースでの `CREATE DATABASE` アクセス許可か、`CREATE ANY DATABASE` または `ALTER ANY DATABASE` のアクセス許可が必要です。  
  
 既存のデータベースの照合順序を変更するには、データベースに対する `ALTER` アクセス許可が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-set-or-change-the-database-collation"></a>データベースの照合順序を設定または変更するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続して、そのインスタンスを展開します。次に、 **[データベース]** を展開します。  
  
2.  新しいデータベースを作成する場合は、 **[データベース]** を右クリックし、 **[新しいデータベース]** をクリックします。 既定の照合順序を使用しない場合は、 **[オプション]** ページをクリックし、 **[照合順序]** ボックスの一覧から照合順序を選択します。  
  
     データベースが既に存在する場合は、使用するデータベースを右クリックし、 **[プロパティ]** をクリックします。 **[オプション]** ページをクリックし、 **[照合順序]** ボックスの一覧から照合順序を選択します。  
  
3.  終了したら **[OK]** をクリックします。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-set-the-database-collation"></a>データベースの照合順序を設定するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例は、 [COLLATE](~/t-sql/statements/collations.md) 句を使用して照合順序名を指定する方法を示しています。 この例は、 `MyOptionsTest` 照合順序を使用する `Latin1_General_100_CS_AS_SC` を作成します。 データベースを作成したら、 `SELECT` ステートメントを実行して設定を検証します。  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
#### <a name="to-change-the-database-collation"></a>データベースの照合順序を変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例は、 [ALTER DATABASE](~/t-sql/statements/collations.md) ステートメントで [COLLATE](../../t-sql/statements/alter-database-transact-sql.md) 句を使用して照合順序名を変更する方法を示しています。 `SELECT` ステートメントを実行して変更を確認します。  
  
```sql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [SQL Server 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)   
 [Windows 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)   
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [照合順序の優先順位 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
