---
title: JDBC 基本データ型の使用
description: Microsoft JDBC Driver for SQL Server では、SQL Server データ型を Java で認識できる形式に変換するために、JDBC 基本データ型が使用されます。
ms.custom: ''
ms.date: 08/24/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3c26c3c065ddf415d966c8fd3613e284c3c7a2b6
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806998"
---
# <a name="using-basic-data-types"></a>基本データ型の使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、JDBC の基本データ型を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を Java プログラミング言語によって認識できる形式に変換します。この逆の変換も行います。 JDBC ドライバー は **SQLXML** データ型を含む JDBC 4.0 api および **NCHAR**、 **NVARCHAR**、 **LONGNVARCHAR**、そして **NCLOB** のような National (Unicode) データ型のサポートを提供します。  
  
## <a name="data-type-mappings"></a>データ型マッピング

次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、JDBC、および Java プログラミング言語の基本データ型間で行われる既定のマッピングを示しています。  
  
| SQL Server 型   | JDBC 型 (java.sql.Types)                        | Java 言語型          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| bigint             | bigint                                             | long                         |
| binary             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | boolean                      |
| char               | CHAR                                               | String                       |
| date               | DATE                                               | java.sql.Date                |
| datetime<sup>3</sup>          | timestamp                               | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset<sup>2</sup> | microsoft.sql.Types.DATETIMEOFFSET         | microsoft.sql.DateTimeOffset |
| decimal            | DECIMAL                                            | java.math.BigDecimal         |
| float              | DOUBLE                                             | double                       |
| image              | LONGVARBINARY                                      | byte[]                       |
| INT                | INTEGER                                            | INT                          |
| money              | DECIMAL                                            | java.math.BigDecimal         |
| nchar              | CHAR<br /><br /> NCHAR (Java SE 6.0)               | String                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String                       |
| numeric            | NUMERIC                                            | java.math.BigDecimal         |
| nvarchar           | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| real               | real                                               | float                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| smallint           | SMALLINT                                           | short                        |
| smallmoney         | DECIMAL                                            | java.math.BigDecimal         |
| text               | LONGVARCHAR                                        | String                       |
| time               | TIME<sup>1</sup>                                   | java.sql.Time<sup>1</sup>            |
| timestamp          | BINARY                                             | byte[]                       |
| tinyint            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| UNIQUEIDENTIFIER   | CHAR                                               | String                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | String                       |
| varchar(max)       | VARCHAR                                            | String                       |
| xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Object                       |
| geometry           | VARBINARY                                          | byte[]                       |
| geography          | VARBINARY                                          | byte[]                       |
  
<sup>1</sup> 時刻の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を持つ java.sql.Time を使用する場合は、**sendTimeAsDatetime** 接続プロパティを false に設定します。  
  
<sup>2</sup> [DateTimeOffset Class](reference/datetimeoffset-class.md) で **datetimeoffset** の値にプログラムでアクセスできます。  
  
<sup>3</sup> SQL Server 2016 以降、datetime 列からの値を比較するために java.sql.Timestamp 値を使用することができなくなりました。 この制限は、datetime を datetime2 に異なるように変換し、値が同じでなくなるサーバー側の変更に起因するものです。 この問題を回避するには、datetime 列を datetime2(3) に変更するか、java.sql.Timestamp ではなく String を使用するか、データベースの互換性レベルを 120 以下に変更します。
  
以下のセクションでは、JDBC ドライバーと基本データ型の使用方法の例を示します。 Java アプリケーションの基本データ型の使用方法の詳細例については、「[基本データ型のサンプル](basic-data-types-sample.md)」をご覧ください。  
  
## <a name="retrieving-data-as-a-string"></a>文字列としてのデータの取得

文字列として参照するために JDBC 基本データ型にマップされるデータ ソースからデータを取得する必要がある場合、または厳密に型指定されたデータを必要としない場合は、次のように [SQLServerResultSet](reference/sqlserverresultset-class.md) クラスの [getString](reference/getstring-method-sqlserverresultset.md) メソッドを使用できます。  
  
[!code[JDBC#UsingBasicDataTypes1](codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>データ型によるデータの取得

データ ソースからデータを取得する必要があり、取得するデータの型がわかっている場合は、SQLServerResultSet クラスのいずれかの get\<Type> メソッドを使用します。これらは、"*getter メソッド*" とも呼ばれます。 get\<Type> メソッドでは、次のように列名または列インデックスを使用できます。  
  
[!code[JDBC#UsingBasicDataTypes2](codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> getUnicodeStream メソッドおよび小数点以下桁数付きの getBigDecimal メソッドは、JDBC ドライバーでは非推奨とされているため、サポートされていません。

## <a name="updating-data-by-data-type"></a>データ型によるデータの更新

データ ソースのフィールドの値を更新する必要がある場合は、SQLServerResultSet クラスのいずれかの update\<Type> メソッドを使用します。 次の例では、[updateInt](reference/updateint-method-sqlserverresultset.md) メソッドを [updateRow](reference/updaterow-method-sqlserverresultset.md) メソッドと組み合わせて使用し、データ ソース内のデータを更新します。  
  
[!code[JDBC#UsingBasicDataTypes3](codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> JDBC ドライバーは、127 文字を超える列名の SQL Server の列を更新できません。 列名が 127 文字を超える列を更新しようとすると、例外がスローされます。  
  
## <a name="updating-data-by-parameterized-query"></a>パラメーター化クエリによるデータの更新

パラメーター化クエリを使用してデータ ソースのデータを更新する必要がある場合は、[SQLServerPreparedStatement](reference/sqlserverpreparedstatement-class.md) クラスのいずれかの set\<Type> メソッドを使用して、パラメーターのデータ型を設定できます。これらは、"*setter メソッド*" とも呼ばれます。 次の例では、[prepareStatement](reference/preparestatement-method-sqlserverconnection.md) メソッドを使用して、パラメーター化クエリをプリコンパイルし、[setString](reference/setstring-method-sqlserverpreparedstatement.md) メソッドを使用してパラメーターの文字列値を設定してから、[executeUpdate](reference/executeupdate-method.md) メソッドを呼び出します。  
  
[!code[JDBC#UsingBasicDataTypes4](codesnippet/Java/using-basic-data-types_4.java)]  
  
パラメーター化されたクエリの詳細については、「[パラメーターがある SQL ステートメントの使用](using-an-sql-statement-with-parameters.md)」を参照してください。  

## <a name="passing-parameters-to-a-stored-procedure"></a>ストアド プロシージャにパラメーターを渡す

入力されたパラメーターをストアド プロシージャに渡す必要がある場合は、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスのいずれかの set\<Type> メソッドを使用して、インデックスまたは名前でパラメーターを設定できます。 次の例では、[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) メソッドを使用してストアド プロシージャへの呼び出しを設定し、[setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) メソッドを使用して呼び出し用のパラメーターを設定してから、[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) メソッドを呼び出します。  
  
[!code[JDBC#UsingBasicDataTypes5](codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> この例では、結果セットはストアド プロシージャの実行結果で返されます。

JDBC ドライバーでストアド プロシージャと入力パラメーターを使用する方法の詳細については、「[入力パラメーターがあるストアド プロシージャの使用](using-a-stored-procedure-with-input-parameters.md)」を参照してください。  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>ストアド プロシージャからのパラメーターの取得

ストアド プロシージャからパラメーターを取得する必要がある場合は、まず SQLServerCallableStatement クラスの [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) メソッドを使用して名前またはインデックスで out パラメーターを登録し、ストアド プロシージャへの呼び出しを実行してから、返された out パラメーターを適切な変数に割り当てる必要があります。 次の例では、prepareCall メソッドを使用してストアド プロシージャへの呼び出しを設定し、registerOutParameter メソッドを使用して out パラメーターを設定します。次に、[setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) メソッドを使用して呼び出し用のパラメーターを設定してから、executeQuery メソッドを呼び出します。 ストアド プロシージャの out パラメーターによって返される値は、[getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) メソッドを使用して取得します。  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> out パラメーターが返されるだけでなく、ストアド プロシージャの実行結果により作成された結果セットが返されることもあります。  
  
JDBC ドライバーでストアド プロシージャと出力パラメーターを使用する方法の詳細については、「[出力パラメーターがあるストアド プロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)」を参照してください。  

## <a name="see-also"></a>関連項目

[JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
