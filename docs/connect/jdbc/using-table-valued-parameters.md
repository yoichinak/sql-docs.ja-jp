---
title: テーブル値パラメーターの使用
description: テーブル値パラメーターを使用すると、1 つのパラメーター化コマンドで、クライアントから SQL Server に複数行のデータを効率的に送信することができます。
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eac620d522408ff9fb4de5550d92cfcbd0f3ec4a
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727473"
---
# <a name="using-table-valued-parameters"></a>テーブル値パラメーターの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

テーブル値パラメーターは、複数行のデータをクライアント アプリケーションから SQL Server に簡単にマーシャリングするための手段です。複数のラウンド トリップや、データ処理用の特別なサーバー側ロジックは必要ありません。 テーブル値パラメーターを使用すると、クライアント アプリケーションで複数行のデータをカプセル化してサーバーに送信する処理を 1 つのパラメーター化コマンドで実行できます。 受信データ行はテーブル変数に格納され、Transact-SQL を使用して操作できます。  
  
テーブル値パラメーターの列値には、Transact-SQL の標準的な SELECT ステートメントを使ってアクセスできます。 テーブル値パラメーターは厳密に型指定されており、その構造が自動的に検証されます。 テーブル値パラメーターのサイズは、サーバーのメモリによってのみ制限されます。  
  
> [!NOTE]  
> テーブル値パラメーターのサポートは、Microsoft JDBC Driver 6.0 for SQL Server 以降で利用できます。
>
> テーブル値パラメーターでデータを返すことはできません。 テーブル値パラメーターは入力専用です。OUTPUT キーワードはサポートされていません。  
  
 テーブル値パラメーターの詳細については、次のリソースを参照してください。  
  
| リソース                                                                                                             | 説明                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| SQL Server オンライン ブックの[テーブル値パラメーター (データベース エンジン)](/previous-versions/sql/sql-server-2008/bb510489(v=sql.100)) | テーブル値パラメーターを作成して使用する方法について説明します                             |
| SQL Server オンライン ブックの「[ユーザー定義テーブル型](/previous-versions/sql/sql-server-2008/bb522526(v=sql.100))」                  | テーブル値パラメーターを宣言する際に使用するユーザー定義テーブル型について説明します |
| CodePlex の「[Microsoft SQL Server データベース エンジン](https://go.microsoft.com/fwlink/?LinkId=120507)」セクション        | SQL Server の機能の使用方法を示すサンプルがあります  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>以前のバージョンの SQL Server で複数の行を渡す  

SQL Server 2008 にテーブル値パラメーターが導入されるまでは、複数行データをストアド プロシージャまたはパラメーター化 SQL コマンドに渡す方法は限られていました。 開発者が選択できる複数の行をサーバーに渡すためのオプションを次に示します。  
  
- 複数のデータ列とデータ行の値を表すには、一連の個別のパラメーターを使用します。 このメソッドを使用して渡すことができるデータの量は、許可されているパラメーター数によって制限されます。 SQL Server プロシージャが持つことのできるパラメーター数は最大 2,100 です。 これらの個々の値をテーブル変数または一時テーブルにまとめて処理するには、サーバー側ロジックが必要です。  
  
- 複数のデータ値を区切り文字列または XML ドキュメントにバンドルし、それらのテキスト値をプロシージャまたはステートメントに渡します。 これを行うには、そのプロシージャまたはステートメントに、データ構造の検証と値のバンドルの解除に必要なロジックが含まれている必要があります。  
  
- 複数の行に影響を及ぼす、データを変更するための一連の SQL ステートメントを個別に作成します。 サーバーへの変更の送信は個別に行うことも、グループにまとめることもできます。 ただし、複数のステートメントがまとめてバッチ送信された場合でも、サーバーでは各ステートメントが個別に実行されます。  
  
- bcp ユーティリティ プログラムまたは [SQLServerBulkCopy](using-bulk-copy-with-the-jdbc-driver.md) を使用して、多数のデータ行をテーブルに読み込みます。 この手法は非常に効率的ですが、サーバー側の処理は、データが一時テーブルまたはテーブル変数に読み込まれない限りサポートされません。
  
## <a name="creating-table-valued-parameter-types"></a>テーブル値パラメーターの型の作成  

テーブル値パラメーターは、Transact-SQL の `CREATE TYPE` ステートメントを使用して定義された厳密に型指定されたテーブルの構造に基づいています。 クライアント アプリケーションでテーブル値パラメーターを使用するには、まず SQL Server でテーブル型を作成し、その構造を定義する必要があります。 テーブル型の作成の詳細については、SQL Server オンライン ブックの「[ユーザー定義テーブル型](/previous-versions/sql/sql-server-2008/bb522526(v=sql.100))」を参照してください。  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

テーブル型を作成したら、その型に基づいてテーブル値パラメーターを宣言できます。 次の Transact-SQL フラグメントは、ストアド プロシージャ定義の中でテーブル値パラメーターを宣言する方法を示しています。 テーブル値パラメーターを宣言するには、`READONLY` キーワードが必要であることに注意してください。  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>テーブル値パラメーターを使用したデータの変更 (Transact-SQL)  

1 つのステートメントを実行することで、テーブル値パラメーターを、複数の行に影響を与えるセットベースのデータ変更で使用できます。 たとえば、テーブル値パラメーター内のすべての行を選択して、データベース テーブルに挿入できます。また、テーブル値パラメーターを更新対象テーブルに結合して、更新ステートメントを作成することもできます。  
  
次の Transact-SQL UPDATE ステートメントは、テーブル値パラメーターを Categories テーブルに結合して使用する方法を示しています。 FROM 句の中でテーブル値パラメーターを JOIN と共に使用する場合は、次に示すように、別名も使用する必要があります。ここでは、テーブル値パラメーターは "ec" という別名になっています。  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

この Transact-SQL の例は、単一のセット ベース操作で INSERT を実行するためにテーブル値パラメーターから行を選択する方法を示しています。

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>テーブル値パラメーターの制限

テーブル値パラメーターにはいくつかの制限があります。  
  
- テーブル値パラメーターをユーザー定義の関数に渡すことはできません。  
  
- テーブル値パラメーターでは、UNIQUE または PRIMARY KEY 制約をサポートするためにのみインデックスを設定できます。 SQL Server では、テーブル値パラメーターの統計が保持されません。  
  
- テーブル値パラメーターは Transact-SQL コードの中では読み取り専用です。 テーブル値パラメーターの行の列値は更新できません。また、行の挿入や削除もできません。 テーブル値パラメーターのストアド プロシージャまたはパラメーター化されたステートメントに渡すデータを変更するには、そのデータを一時テーブルまたはテーブル変数に挿入する必要があります。  
  
- ALTER TABLE ステートメントを使用して、テーブル値パラメーターの設計を変更することはできません。

- ラージ オブジェクトは、テーブル値パラメーターでストリームできます。  
  
## <a name="configuring-a-table-valued-parameter"></a>テーブル値パラメーターの構成

Microsoft JDBC Driver 6.0 for SQL Server 以降では、テーブル値パラメーターが、パラメーター化されたステートメントまたはパラメーター化されたストアド プロシージャでサポートされるようになりました。 テーブル値パラメーターは、SQLServerDataTable から、ResultSet から、またはユーザーが指定した ISQLServerDataRecord インターフェイスの実装から設定できます。 用意されたクエリにテーブル値パラメーターを設定する場合、指定する型名は、サーバーで以前に作成された互換性のある型の名前と一致している必要があるます。  
  
次の 2 つのコードは、データを挿入するためにテーブル値パラメーターを構成する方法として、SQLServerPreparedStatement を指定する方法と SQLServerCallableStatement を指定する方法を示しています。 ここで、sourceTVPObject には、QLServerDataTable、ResultSet、または ISQLServerDataRecord オブジェクトを指定できます。 これらの例では、接続がアクティブな接続オブジェクトであることを想定しています。  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement("INSERT INTO dbo.Categories SELECT * FROM ?");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```

```java
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```

> [!NOTE]  
> テーブル値パラメーターの設定に使用できるすべての API の一覧については、下記のセクション「**JDBC ドライバー用のテーブル値パラメーターの API**」を参照してください。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>テーブル値パラメーターを SQLServerDataTable オブジェクトとして渡す  

Microsoft JDBC Driver 6.0 for SQL Server 以降では、SQLServerDataTable クラスがリレーショナル データのインメモリ テーブルを表すようになりました。 この例では、SQLServerDataTable オブジェクトを使用して、インメモリ データからテーブル値パラメーターを構築する方法を示しています。 このコードでは、まず SQLServerDataTable オブジェクトを作成し、そのスキーマを定義してテーブルにデータを設定します。 次にこのコードでは、このデータ テーブルをテーブル値パラメーターとして SQL Server に渡す SQLServerPreparedStatement を構成します。  

```java
/* Assumes connection is an active Connection object. */

// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");
sourceDataTable.addRow(2, "CategoryNameValue2");
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```

> [!NOTE]  
> テーブル値パラメーターの設定に使用できるすべての API の一覧については、下記のセクション「**JDBC ドライバー用のテーブル値パラメーターの API**」を参照してください。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>テーブル値パラメーターを ResultSet オブジェクトとして渡す  

この例では、ResultSet からテーブル値パラメーターにデータの行をストリームする方法を示します。 このコードでは、まず SQLServerDataTable オブジェクト内のソース テーブルからデータを取得し、そのスキーマを定義してテーブルにデータを設定します。 次にこのコードでは、このデータ テーブルをテーブル値パラメーターとして SQL Server に渡す SQLServerPreparedStatement を構成します。  

```java
/* Assumes connection is an active Connection object. */

// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  

// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```

> [!NOTE]  
> テーブル値パラメーターの設定に使用できるすべての API の一覧については、下記のセクション「**JDBC ドライバー用のテーブル値パラメーターの API**」を参照してください。  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>テーブル値パラメーターを ISQLServerDataRecord オブジェクトとして渡す  

Microsoft JDBC Driver 6.0 for SQL Server 以降では、テーブル値パラメーターを使用してデータをストリームするための新しいインターフェイス ISQLServerDataRecord が使用できるようになりました (ユーザーによってその実装がどのように用意されるかによって変わります)。 次の例は、ISQLServerDataRecord インターフェイスを実装する方法と、それをテーブル値パラメーターとして渡す方法を示しています。 わかりやすくするために、次の例では、ハードコードされた値を含む 1 つの行だけをテーブル値パラメーターに渡します。 ユーザーがこのインターフェイスを実装して、テキスト ファイルなどの任意のソースから行をストリームすることが理想的です。  

```java
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }
}

// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```

> [!NOTE]  
> テーブル値パラメーターの設定に使用できるすべての API の一覧については、下記のセクション「**JDBC ドライバー用のテーブル値パラメーターの API**」を参照してください。

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC ドライバー用のテーブル値パラメーターの API

### <a name="sqlservermetadata"></a>SQLServerMetaData

このクラスは、列のメタデータを表します。 これは、列のメタデータをテーブル値パラメーターに渡すために ISQLServerDataRecord インターフェイスで使用されます。 このクラスのメソッドは次のとおりです。  

| 名前                                                                                                                                                                             | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData(String columnName, int sqlType, int precision, int scale, boolean useServerDefault, boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | 指定された列名、SQL 型、有効桁数、小数点以下桁数、およびサーバーの既定値を使用して、SQLServerMetaData の新しいインスタンスを初期化します。 この形式のコンストラクターは、テーブル値パラメーター内で列が一意であるかどうか、列の並べ替え順序、および並べ替え列の序数を指定できるようにすることで、テーブル値パラメーターをサポートします。 <br/><br/>useServerDefault - この列で既定のサーバー値を使用する必要があるかどうかを指定します。既定値は false です。<br>isUniqueKey - テーブル値パラメーター内の列が一意であるかどうかを示します。既定値は false です。<br>sortOrder - 列の並べ替え順序を示します。既定値は SQLServerSortOrder.Unspecified です。<br>sortOrdinal - 並べ替え列の序数を指定します。sortOrdinal は 0 から始まります。既定値は -1 です。 |
| public SQLServerMetaData( String columnName, int sqlType)                                                                                                                        | 列名と SQL 型を使用して、SQLServerMetaData の新しいインスタンスを初期化します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData( String columnName, int sqlType, int length)                                                                                                                        | 列名、SQL 型、および長さ (文字列データの場合) を使用して、SQLServerMetaData の新しいインスタンスを初期化します。 長さは、大きな文字列を 4000 文字未満の長さの文字列から区別するために使用されます。 JDBC ドライバーのバージョン7.2 で導入されました。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData( String columnName, int sqlType, int precision, int scale)                                                                                              | 列名、SQL 型、有効桁数、および小数点以下桁数を使用して、SQLServerMetaData の新しいインスタンスを初期化します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | 別の SQLServerMetaData オブジェクトから SQLServerMetaData の新しいインスタンスを初期化します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | 列名を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | Java SQL 型を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision()                                                                                                                                                        | 列に渡される型の有効桁数を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | 列に渡される型の小数点以下桁数を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | 並べ替え順を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | 並べ替えの序数を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | 列が一意であるかどうかを返します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | 列が既定のサーバー値を使用するかどうかを返します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

並べ替え順序を定義する列挙型。 有効値は、Ascending (昇順)、Descending (降順)、および Unspecified (未指定) です。
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

このクラスは、テーブル値パラメーターで使用されるインメモリ データ テーブルを表します。 このクラスのメソッドは次のとおりです。  

| 名前                                                          | 説明                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | SQLServerDataTable の新しいインスタンスを初期化します。    |
| public Iterator<Entry\<Integer, Object[]>> getIterator()      | データ テーブルの行の反復子を取得します。 |
| public void addColumnMetadata(String columnName, int sqlType) | 指定された列のメタデータを追加します。              |
| public void addColumnMetadata(SQLServerDataColumn column)     | 指定された列のメタデータを追加します。              |
| public void addRow(Object... values)                          | データ テーブルに 1 行のデータを追加します。              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | このデータ テーブルの列メタデータを取得します。       |
| public void clear()                                           | このデータ テーブルをクリアします。                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

このクラスは、SQLServerDataTable によって表されるインメモリ データ テーブルの列を表します。 このクラスのメソッドは次のとおりです。  

| 名前                                                       | 説明                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn(String columnName, int sqlType) | 列名と型を使用して、SQLServerDataColumn の新しいインスタンスを初期化します。 |
| public String getColumnName()                              | 列名を取得します。                                                       |
| public int getColumnType()                                 | 列の型を取得します。                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

このクラスは、ユーザーがテーブル値パラメーターにデータをストリームするために実装できるインターフェイスを表します。 このインターフェイスのメソッドは次のとおりです。  
  
| 名前                                                    | 説明                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | 指定された列インデックスの列メタデータを取得します。                                               |
| public int getColumnCount();                            | 列数の合計数を取得します。                                                                  |
| public Object[] getRowData();                           | オブジェクトの配列として、現在の行のデータを取得します。                                          |
| public boolean next();                                  | 次の行に移動します。 移動が正常に行われ、次の行が存在する場合は True を返します。それ以外の場合は false を返します。 |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

次のメソッドは、テーブル値パラメーターの引き渡しをサポートするために、このクラスに追加されました。  

| 名前                                                                                                    | 説明                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | テーブル値パラメーターにデータ テーブルを設定します。 parameterIndex はパラメーター インデックス、tvpName はテーブル値パラメーターの名前、tvpDataTable はソース データ テーブル オブジェクトです。                                                                                                          |
| public final void setStructured(int parameterIndex, String tvpName, ResultSet tvpResultSet)             | テーブル値パラメーターに、別のテーブルから取得された ResultSet を設定します。 parameterIndex はパラメーター インデックス、tvpName はテーブル値パラメーターの名前、tvpResultSet はソース結果セット オブジェクトです。                                                                               |
| public final void setStructured(int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | テーブル値パラメーターに ISQLServerDataRecord オブジェクトを設定します。 ISQLServerDataRecord はデータをストリームするために使用され、その使用方法はユーザーが決定します。 parameterIndex はパラメーター インデックス、tvpName はテーブル値パラメーターの名前、tvpDataRecord は ISQLServerDataRecord オブジェクトです。 |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

次のメソッドは、テーブル値パラメーターの引き渡しをサポートするために、このクラスに追加されました。  
  
| 名前                                                                                                        | 説明                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | ストアド プロシージャに渡されるテーブル値パラメーターにデータ テーブルを設定します。 paratemeterName はパラメーターの名前、tvpName は TVP 型の名前、tvpDataTable はデータ テーブル オブジェクトです。                                                                                                                 |
| public final void setStructured(String paratemeterName, String tvpName, ResultSet tvpResultSet)             | ストアド プロシージャに渡されるテーブル値パラメーターに、別のテーブルから取得された ResultSet を設定します。 paratemeterName はパラメーターの名前、tvpName は TVP 型の名前、tvpResultSet はソース結果セット オブジェクトです。                                                                              |
| public final void setStructured(String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | ストアド プロシージャに渡されるテーブル値パラメーターに ISQLServerDataRecord オブジェクトを設定します。 ISQLServerDataRecord はデータをストリームするために使用され、その使用方法はユーザーが決定します。 paratemeterName はパラメーターの名前、tvpName は TVP 型の名前、tvpDataTable はデータ テーブル オブジェクトです。tvpDataRecord は ISQLServerDataRecord オブジェクトです。 |

## <a name="see-also"></a>関連項目

[JDBC ドライバーの概要](overview-of-the-jdbc-driver.md)