---
title: データ型変換について
description: JDBC Driver for SQL Server で JDBC データ型とデータベース データ型の間でデータ型変換を処理するしくみを具体的に説明します。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 266db3efac0fb737ccb36900ef3b27f24c8c8888
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081681"
---
# <a name="understanding-data-type-conversions"></a>データ型変換について

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Java プログラミング言語のデータ型を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型へ容易に変換できるようにするため、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] には、JDBC の仕様で必要とされるデータ型変換が用意されています。 さらに高い柔軟性を得るために、すべての型を **Object**、**String**、および **byte[]** のデータ型との間で変換できるようになりました。

## <a name="getter-method-conversions"></a>getter メソッドの変換

次の図は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型に基づいて、[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスの get\<Type>() メソッド用の JDBC ドライバーの変換マップ、および [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスの get\<Type> メソッドでサポートされている変換を示しています。

![JDBC から SQL Server 型への変換のマトリックス](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")

JDBC ドライバーの getter メソッドでサポートされている変換には、次の 3 つのカテゴリがあります。

- **データ損失なし (x)**: getter 型が、基になるサーバーの型と同じか、またはそれより小さい場合の変換です。 たとえば、基になるサーバーの decimal 列で getBigDecimal を呼び出すとき、変換は必要ありません。

- **変換 (y)**: サーバーの数値型から Java 言語型への変換です。変換は通常の変換で、Java 言語変換ルールに従って行われます。 これらの変換では、有効桁数は四捨五入されることはなく常に切り捨てられます。オーバーフローは変換後の型の剰余として処理され、前より小さくなります。 たとえば、"1.9999" を含む基になる **decimal** 列で getInt を呼び出すと、"1" が返されます。基になる **decimal** 値が "3000000000" の場合、**int** 値はオーバーフローして "-1294967296" となります。

- **データに依存 (z)**: 基になる文字型から数値型への変換では、文字型は数値型に変換できる値を含んでいる必要があります。 これ以外の変換は行われません。 値が getter 型には大きすぎる場合、その値は有効ではありません。 たとえば、"53" を含む varchar(50) 列で getInt が呼び出された場合、値は **int** として返されます。基になる値が "xyz" または "3000000000" の場合は、エラーがスローされます。

**binary** 列、**varbinary** 列、**varbinary (max)** 列、**image** 列のいずれかのデータ型に対して getString が呼び出されると、値が 16 進数の文字列値として返されます。

## <a name="updater-method-conversions"></a>updater メソッドの変換

[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスの update\<Type>() メソッドに渡された、Java で型指定されたデータには、次の変換が適用されます。

![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")

JDBC ドライバーの updater メソッドでサポートされている変換には、次の 3 つのカテゴリがあります。

- **データ損失なし (x)**: updater 型が、基になるサーバーの型と同じか、またはそれより小さい場合の変換です。 たとえば、基になるサーバーの decimal 列で updateBigDecimal を呼び出すとき、変換は必要ありません。

- **変換 (y)**: サーバーの数値型から Java 言語型への変換です。変換は通常の変換で、Java 言語変換ルールに従って行われます。 これらの変換では、有効桁数は四捨五入されることはなく常に切り捨てられます。オーバーフローは変換後の型の剰余として処理され、変換前より小さくなります。 たとえば、"1.9999" を含む基になる **int** 列で updateDecimal を呼び出すと、"1" が返されます。基になる **decimal** 値が "3000000000" の場合、**int** 値はオーバーフローして "-1294967296" となります。

- **データに依存 (z)**: 基になるデータ型を別のデータ型に変換するには、前者の型が後者の型に変換可能な値を含んでいることが必要です。 これ以外の変換は行われません。 値が getter 型には大きすぎる場合、その値は有効ではありません。 たとえば、"53" が格納された int 列に対して updateString を呼び出した場合、更新は成功しますが、基になる文字列値が "foo" や "3000000000" であった場合は、エラーがスローされます。

**binary** 列、**varbinary** 列、**varbinary (max)** 列、**image** 列のいずれかのデータ型に対して updateString が呼び出されると、値は 16 進数の文字列値として処理されます。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の列データ型が **XML** の場合、データ値は有効な **XML** であることが必要です。 updateBytes、updateBinaryStream、updateBlob のいずれかのメソッドを呼び出す場合、データ値は、XML 文字の 16 進形式の文字列表記である必要があります。 たとえば、次のように入力します。

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

XML 文字に特定の文字エンコードが使用されている場合は、バイト順マーク (BOM) が必要です。

## <a name="setter-method-conversions"></a>setter メソッドの変換

[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスおよび [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスの set\<Type>() メソッドに渡された、Java で型指定されたデータには、次の変換が適用されます。

![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")

サーバーはすべての変換を試みて、変換に失敗した場合はエラーを返します。

**String** データ型の場合、値は **VARCHAR** の長さを超えると **LONGVARCHAR** にマップされます。 同様に、値がサポートされている長さの **NVARCHAR**を超えると、**NVARCHAR** は **LONGNVARCHAR** にマップされます。 **byte[]** の場合も同様です。 **VARBINARY** より長い値は、**LONGVARBINARY** なります。

JDBC ドライバーの setter メソッドでサポートされている変換には、次の 2 つのカテゴリがあります。

- **データ損失なし (x)**: setter 型が、基になるサーバーの型と同じか、またはそれより小さい場合の数値変換です。 たとえば、基になるサーバーの **decimal** 列で setBigDecimal を呼び出すとき、変換は必要ありません。 数値を文字に変換する場合、Java の **numeric** データ型は **String** に変換されます。 たとえば、varchar(50) 列で "53" の値を使用して setDouble を呼び出すと、変換先の列に文字列値 "53" が作成されます。

- **変換 (y)**: Java の **numeric** 型から基になるサーバーの **numeric** 型への変換です。これは変換前より小さくなります。 この変換は通常の変換で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変換規則に従って行われます。 有効桁数は常に切り捨てられ、四捨五入されることはありません。オーバーフローするとサポートされていない変換のエラーがスローされます。 たとえば、"1.9999" の値を持つ基になる整数列に updateDecimal を使用すると、変換先の列は "1" になりますが、"3000000000" が渡されるとドライバーはエラーをスローします。

- **データに依存 (z)**: Java の **String** 型から基になる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型への変換は、次の条件に依存します。ドライバーが **String** 値を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送信し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が必要に応じて変換を実行します。 sendStringParametersAsUnicode が true に設定されており、なおかつ、基になる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型が **image** である場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では **nvarchar** の **image** への変換が許可されず、SQLServerException がスローされます。 sendStringParametersAsUnicode が false に設定されており、なおかつ、基になる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型が **image** である場合、**varchar** から **image** への変換が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって許可され、例外はスローされません。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は変換を行い、問題が発生すると JDBC ドライバーにエラーを返します。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の列データ型が **XML** の場合、データ値は有効な **XML** であることが必要です。 updateBytes、updateBinaryStream、updateBlob のいずれかのメソッドを呼び出す場合、データ値は、XML 文字の 16 進形式の文字列表記である必要があります。 たとえば、次のように入力します。

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

XML 文字に特定の文字エンコードが使用されている場合は、バイト順マーク (BOM) が必要です。

## <a name="conversions-on-setobject"></a>setObject での変換

> [!NOTE]  
> Microsoft JDBC Driver 4.2 for SQL Server (以降) では、JDBC 4.1 と 4.2 がサポートされています。 4.1、4.2 のデータ型マッピングと変換の詳細については、下記の情報に加えて、「[JDBC ドライバーの JDBC 4.1 への準拠](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)」と「[JDBC ドライバーの JDBC 4.2 への準拠](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)」を参照してください。

[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスの setObject(\<Type>) メソッドに渡された、Java で型指定されたデータには、次の変換が適用されます。

![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")

変換後の型が指定されていない setObject メソッドでは、既定のマッピングが使用されます。 **String** データ型の場合、値は **VARCHAR** の長さを超えると **LONGVARCHAR** にマップされます。 同様に、値がサポートされている長さの **NVARCHAR**を超えると、**NVARCHAR** は **LONGNVARCHAR** にマップされます。 **byte[]** の場合も同様です。 **VARBINARY** より長い値は、**LONGVARBINARY** なります。

JDBC ドライバーの setObject メソッドでサポートされている変換には、次の 3 つのカテゴリがあります。

- **データ損失なし (x)**: setter 型が、基になるサーバーの型と同じか、またはそれより小さい場合の数値変換です。 たとえば、基になるサーバーの **decimal** 列で setBigDecimal を呼び出すとき、変換は必要ありません。 数値を文字に変換する場合、Java の **numeric** データ型は **String** に変換されます。 たとえば、varchar(50) 列で "53" の値を使用して setDouble を呼び出すと、変換先の列に文字列値 "53" が作成されます。

- **変換 (y)**: Java の **numeric** 型から基になるサーバーの **numeric** 型への変換です。これは変換前より小さくなります。 この変換は通常の変換で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変換規則に従って行われます。 有効桁数は常に切り捨てられ、四捨五入されることはありません。オーバーフローするとサポートされていない変換のエラーがスローされます。 たとえば、"1.9999" の値を持つ基になる整数列に updateDecimal を使用すると、変換先の列は "1" になりますが、"3000000000" が渡されるとドライバーはエラーをスローします。

- **データに依存 (z)**: Java の **String** 型から基になる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型への変換は、次の条件に依存します。ドライバーが **String** 値を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送信し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が必要に応じて変換を実行します。 sendStringParametersAsUnicode 接続プロパティが true に設定されており、なおかつ、基になる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型が **image** である場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では **nvarchar** の **image** への変換が許可されず、SQLServerException がスローされます。 sendStringParametersAsUnicode が false に設定されており、なおかつ、基になる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型が **image** である場合、**varchar** から **image** への変換が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって許可され、例外はスローされません。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は一括して設定の変換を行い、問題が発生すると JDBC ドライバーにエラーを返します。 クライアント側で行われる変換は例外で、**date**、**time**、**timestamp**、**Boolean**、および **String** の値の場合のみ実行されます。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の列データ型が **XML** の場合、データ値は有効な **XML** であることが必要です。 setObject(byte[], SQLXML)、setObject(inputStream, SQLXML)、setObject(Blob, SQLXML) のいずれかのメソッドを呼び出す場合、データ値は、XML 文字の 16 進形式の文字列表記である必要があります。 たとえば、次のように入力します。

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

XML 文字に特定の文字エンコードが使用されている場合は、バイト順マーク (BOM) が必要です。

## <a name="see-also"></a>関連項目

[JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
