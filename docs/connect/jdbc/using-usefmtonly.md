---
description: UseFmtOnly を使用した ParameterMetaData の取得
title: UseFmtOnly を使用した ParameterMetaData の取得 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 509c88230b8a09933291e5c09d528370cf06caca
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081531"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>UseFmtOnly を使用した ParameterMetaData の取得
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft JDBC Driver for SQL Server には、サーバーからパラメーターのメタデータをクエリする別の方法として、**useFmtOnly** があります。 この機能は、ドライバーのバージョン 7.4 で初めて導入されたものであり、`sp_describe_undeclared_parameters` の既知の問題に対する回避策として必要です。
  
  ドライバーは、主にストアド プロシージャ `sp_describe_undeclared_parameters` を使用してパラメーターのメタデータのクエリを実行します。これは、ほとんどの状況でパラメーター メタデータの取得に推奨される方法です。 ただし、現在、ストアド プロシージャの実行は次のユース ケースでは失敗します。
  
-   Always Encrypted 列に対して
  
-   一時テーブルとテーブル変数に対して
  
-   ビューに対して 
  
  これらのユース ケースに対する提案ソリューションは、ユーザーの SQL クエリでパラメーターとテーブル ターゲットを解析し、`FMTONLY` が有効になっている `SELECT` クエリを実行することです。 次のスニペットを使用すると、機能を視覚化できます。
  
```sql
--create a normal table 'Foo' and a temporary table 'Bar'
CREATE TABLE Foo(c1 int);
CREATE TABLE #Bar(c1 int);

EXEC sp_describe_undeclared_parameters N'SELECT * FROM Foo WHERE c1 = @p0' --works fine
EXEC sp_describe_undeclared_parameters N'SELECT * FROM #Bar WHERE c1 = @p0' --fails with "Invalid object name '#Bar'"

SET FMTONLY ON;
SELECT c1 FROM Foo; --works
SET FMTONLY OFF;
SET FMTONLY ON;
SELECT c1 FROM #Bar; --works
SET FMTONLY OFF;
```
 
## <a name="turning-the-feature-onoff"></a>機能のオン/オフの切り替え 
 **useFmtOnly** 機能は既定ではオフになっています。 ユーザーは、`useFmtOnly=true` を指定すると、接続文字列を使用してこの機能を有効にできます  (例: `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`)。
 
 または、`SQLServerDataSource` から機能を使用することができます。
 ```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName(<server>);
ds.setPortNumber(<port>);
ds.setDatabaseName("<databaseName>");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setUseFmtOnly(true);
try (Connection c = ds.getConnection()) {
    // do work with connection
}
 ```
 
 この機能は、ステートメント レベルでも使用できます。 ユーザーは、`PreparedStatement.setUseFmtOnly(boolean)` を使用して機能のオン/オフを切り替えることができます。
> [!NOTE]  
>  ドライバーでは、ステートメント レベル プロパティが "接続レベル" プロパティより優先されます。

## <a name="using-the-feature"></a>機能の使用
  有効にすると、ドライバーでは、パラメーターのメタデータのクエリを実行するときに、`sp_describe_undeclared_parameters` ではなく、新しい機能の使用を内部的に開始します。 エンド ユーザーがこれ以上操作を行う必要はありません。
```java
final String sql = "INSERT INTO #Bar VALUES (?)";
try (Connection c = DriverManager.getConnection(URL, USERNAME, PASSWORD)) {
    try (Statement s = c.createStatement()) {
        s.execute("CREATE TABLE #Bar(c1 int)");
    }
    try (PreparedStatement p1 = c.prepareStatement(sql); PreparedStatement p2 = c.prepareStatement(sql)) {
        ((SQLServerPreparedStatement) p1).setUseFmtOnly(true);
        ParameterMetaData pmd1 = p1.getParameterMetaData();
        System.out.println(pmd1.getParameterTypeName(1)); // prints int
        ParameterMetaData pmd2 = p2.getParameterMetaData(); // throws exception, Invalid object name '#Bar'
    }
}
```
> [!NOTE]  
>  この機能では、`SELECT/INSERT/UPDATE/DELETE` クエリのみサポートされます。 クエリは、サポートされている 4 つのキーワードのいずれか、または[共通テーブル式](../../t-sql/queries/with-common-table-expression-transact-sql.md)で始まり、サポートされているいずれかのクエリがその後ろに続く必要があります。 共通テーブル式内のパラメーターはサポートされていません。

## <a name="known-issues"></a>既知の問題
  現在、機能には、SQL の解析ロジックの欠陥が原因である問題がいくつかあります。 これらの問題は、機能の今後の更新プログラムで解決される可能性があります。回避策と合わせて以下に説明します。
  
A. '前方宣言' のエイリアスを使用している
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. テーブルに共有列名がある場合、列名があいまいである
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. パラメーターを設定したサブクエリからの SELECT
```sql

CREATE TABLE Foo(c1 int)

SELECT * FROM (SELECT * FROM Foo WHERE c1 = ?) WHERE c1 = ?; --Incorrect syntax near '?'

--Workaround: N/A
```

D. SET 句でのサブクエリ
```sql
CREATE TABLE Foo(c1 int)

UPDATE Foo SET c1 = (SELECT c1 FROM Foo) WHERE c1 = ?; --Incorrect syntax near ')'

--Workaround: Add a 'delimiting' condition
UPDATE Foo SET c1 = (SELECT c1 FROM Foo HAVING (HASH JOIN)) WHERE c1 = ?;
```

## <a name="see-also"></a>関連項目  
 [接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)  
  
