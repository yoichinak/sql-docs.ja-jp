---
title: null 値の処理
description: SQL Server と .NET で null 値を処理する方法と、この値と空の値との違いについて説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 4d11586f380354d0cef98039fbe95d2f9ed3287b
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081461"
---
# <a name="handling-null-values"></a>null 値の処理

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

列の値が不明、または欠落している場合は、リレーショナル データベース内の null 値が使用されます。 null は、空の文字列 (文字型または 日時データ型の場合) でも、0 値 (数値データ型の場合) でもありません。 ANSI SQL-92 の規格では、すべての null が一貫して処理されるように、すべてのデータ型で同じである必要があると規定されています。 <xref:System.Data.SqlTypes> 名前空間では、<xref:System.Data.SqlTypes.INullable> インターフェイスを実装することによって null セマンティクスが提供されます。 <xref:System.Data.SqlTypes> の各データ型には、そのデータ型のインスタンスに割り当てることができる独自の `IsNull` プロパティと `Null` 値があります。  
  
> [!NOTE]
>  .NET Framework バージョン 2.0 と .NET Core バージョン 1.0 では、null 許容型のサポートが導入され、プログラマが値の型を拡張し、基になる型のすべての値を表すことができるようになりました。 これらの CLR null 許容型は、<xref:System.Nullable> 構造体のインスタンスを表します。 この機能は、値の型がボックス化およびボックス化解除されている場合に特に有効であり、オブジェクトの型との互換性が強化されます。 ANSI SQL null は `null` 参照 (または Visual Basic の `Nothing`) と同じようには動作しないため、CLR null 許容型はデータベース null の格納を目的としたものではありません。 データベースの ANSI SQL null 値を操作するには、<xref:System.Data.SqlTypes> ではなく <xref:System.Nullable> null を使用します。 C# での CLR null 許容型の操作の詳細については [null 許容型](/dotnet/csharp/programming-guide/nullable-types/)に関するページを、C# については [null 許容型の使用](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/)に関するページを参照してください。  
  
## <a name="nulls-and-three-valued-logic"></a>null および 3 値ロジック  
列定義で null 値を許可すると、アプリケーションに 3 値ロジックが導入されます。 比較では、次の 3 つの状態のいずれかに評価されます。  
  
- True  
  
- False  
  
- Unknown  
  
null は不明と見なされるため、2 つの null 値を互いに比較しても、値が等しいとは見なされません。 算術演算子を使用した式では、オペランドのいずれかが null である場合は結果も null になります。  
  
## <a name="nulls-and-sqlboolean"></a>null と SqlBoolean  
任意の <xref:System.Data.SqlTypes> 間の比較により、<xref:System.Data.SqlTypes.SqlBoolean> が返されます。 各 `IsNull` に対する `SqlType` 関数では <xref:System.Data.SqlTypes.SqlBoolean> が返され、null 値の確認に使用できます。 次の真理値表は、null 値がある場合に AND、OR、NOT 演算子がどのように機能するかを示しています。 (T=true、F=false、U=不明または null。)  
  
![真理値表](../media/truthtable-bpuedev11.gif "TruthTable_bpuedev11")  
  
### <a name="understanding-the-ansi_nulls-option"></a>ANSI_NULLS オプションについて  
<xref:System.Data.SqlTypes> は、SQL Server で ANSI_NULLS オプションが有効に設定されている場合と同じセマンティクスを提供します。 すべての算術演算子 (+、-、*、/、%)、ビット演算子 (~、&、&#124)、およびほとんどの関数では、プロパティ `IsNull` を除き、オペランドまたは引数が NULL であった場合に NULL を返します。  
  
ANSI SQL-92 標準では、WHERE 句で *columnName* = NULL とすることは認められていません。 SQL Server では、ANSI_NULLS オプションによって、データベース内の既定の null 値の許容と null 値に対する比較の評価の両方が制御されます。 ANSI_NULLS が有効になっている (既定) 場合、null 値をテストする式で IS NULL 演算子を使用する必要があります。 たとえば、ANSI_NULLS を ON にした場合、次の比較では、必ず UNKNOWN が返されます。  
  
```console
colname > NULL  
```  
  
また、null 値を含む変数との比較でも不明となります。  
  
```console
colname > @MyVariable  
```  
  
IS NULL 述語または IS NOT NULL 述語は、NULL 値があるかどうかを調べるのに使用します。 ただし、これを使用すると WHERE 句は複雑になります。 たとえば、AdventureWorks Customer テーブル内の TerritoryID 列では null 値が許可されています。 SELECT ステートメントで特定の値の他に NULL 値の有無も調べるには、IS NULL 述語を使用する必要があります。  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
SQL Server で ANSI_NULLS を無効にすると、等値演算子を使用して null と比較する式を作成できます。 ただし、別の接続ではこの接続の null オプションの設定を回避することはできません。 IS NULL を使用した null 値のテストは、接続の ANSI_NULLS の設定に関係なく常に機能します。  
  
`DataSet` では、ANSI_NULLS のオフ設定はサポートされていません。<xref:System.Data.SqlTypes> における null 値の処理については、常に ANSI SQL-92 標準に準拠しています。  
  
## <a name="assigning-null-values"></a>null 値の割り当て  
null 値は特殊であるため、その格納や割り当てのセマンティクスはシステムおよびストレージ システムの種類によって異なります。 `Dataset` は、異なる種類のストレージ システムで使用されるように設計されています。  
  
このセクションでは、異なる種類のシステムにある <xref:System.Data.DataColumn> の <xref:System.Data.DataRow> に null 値を割り当てるための null セマンティクスについて説明します。  
  
`DBNull.Value`  
この割り当ては、任意の型の `DataColumn` で有効です。 その型が `INullable` を実装している場合、`DBNull.Value` は、厳密に型指定された適切な null 値に強制的に変換されます。  
  
`SqlType.Null`  
すべての <xref:System.Data.SqlTypes> データ型で `INullable` を実装します。 暗黙的なキャスト演算子を使用して、厳密に型指定された null 値を列のデータ型に変換できる場合は、割り当てが行われます。 そうでない場合は、無効なキャスト例外がスローされます。  
  
`null`  
'null' が特定の `DataColumn` データ型で有効な値である場合は、`DbNull.Value` 型 (`Null`) に関連付けられた適切な `INullable` または `SqlType.Null` に強制的に変換されます。  
  
`derivedUdt.Null`  
UDT 列の場合、null 値は常に `DataColumn` に関連付けられた型に基づいて格納されます。 `DataColumn` に関連付けられた UDT が `INullable` を実装しておらず、そのサブクラスで実装している場合を考えてみます。 この場合、派生クラスに関連付けられた厳密に型指定された null 値が割り当てられていれば、null ストレージが常に DataColumn のデータ型と一致するため、型指定されていない `DbNull.Value` として格納されます。  
  
> [!NOTE]
>  `Nullable<T>` または <xref:System.Nullable> 構造体は現在、`DataSet` ではサポートされていません。  
  
### <a name="multiple-column-row-assignment"></a>複数列 (行) の割り当て  
`DataTable.Add`、`DataTable.LoadDataRow`、または行にマップされる <xref:System.Data.DataRow.ItemArray%2A> を受け入れる他の API では、DataColumn の既定値に 'null' を マップします。 配列内のオブジェクトに `DbNull.Value` またはその厳密に型指定された同等の値が含まれている場合は、上記と同じ規則が適用されます。  
  
さらに、`DataRow.["columnName"]` null 値割り当てのインスタンスには次の規則が適用されます。  
  
- 既定の *default* 値は `DbNull.Value` です。ただし、それが厳密に型指定された適切な NULL 値となる、厳密に型指定された NULL 列は例外です。  
  
- XML ファイルへのシリアル化中に null 値が ("xsi:nil" として) 書き出されることはありません。  
  
- 既定値を含む null 以外の値はすべて、XML へのシリアル化中に常に書き出されます。 これは、null 値 (xsi:nil) が明示的であり、既定値が暗黙的である XSD/XML セマンティクスとは異なります (XML にない場合、検証パーサーが関連付けられた XSD スキーマから取得します)。 `DataTable` ではこの逆になり、null 値が暗黙的であり、既定値が明示的です。  
  
- XML 入力から読み取られた各行で欠落している列値にはすべて、NULL が割り当てられます。 <xref:System.Data.DataTable.NewRow%2A> または同様のメソッドを使用して作成された行には、DataColumn の既定値が割り当てられます。  
  
- <xref:System.Data.DataRow.IsNull%2A> メソッドは、`true` と `DbNull.Value` のどちらに対しても `INullable.Null` を返します。  
  
## <a name="assigning-null-values-to-sqltypes"></a>SqlTypes への null 値の割り当て  
任意の <xref:System.Data.SqlTypes> インスタンスの既定値は null です。  
  
<xref:System.Data.SqlTypes> の null 値は型固有であり、`DbNull` などの 1 つの値で表すことはできません。 null 値を確認するには、`IsNull` プロパティを使用します。  
  
null 値は次のコード例に示すように、<xref:System.Data.DataColumn> に割り当てることができます。 null 値は例外をトリガーすることなく、`SqlTypes` 変数に直接割り当てることができます。  
  
### <a name="example"></a>例  
次のコード例では、<xref:System.Data.DataTable> と <xref:System.Data.SqlTypes.SqlInt32> として定義された 2 つの列を含む <xref:System.Data.SqlTypes.SqlString> を作成します。 このコードでは、既知の値の 1 行と null 値の 1 行を追加し、<xref:System.Data.DataTable> を反復処理します。これによって変数に値を割り当て、コンソール ウィンドウに出力を表示します。  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
この例では、次の結果が表示されます。  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>SqlTypes と CLR 型での null 値の比較  
null 値を比較する場合は、`Equals` メソッドが <xref:System.Data.SqlTypes> の null 値を評価する方法と、CLR 型を操作する方法の違いを理解することが重要です。 <xref:System.Data.SqlTypes>`Equals` メソッドはすべて、null 値の評価にデータベース セマンティクスを使用します。値の一方または両方が null である場合は、その比較によって null が得られます。 これに対して、2 つの `Equals` に対して CLR <xref:System.Data.SqlTypes> メソッドを使用すると、両方が null である場合に true が得られます。 これは、CLR `String.Equals` メソッドなどのインスタンス メソッドの使用と、静的/共有メソッド `SqlString.Equals` の使用の違いを反映しています。  
  
次の例は、`SqlString.Equals` メソッドと `String.Equals` メソッドにそれぞれ null 値のペアを渡し、次に空の文字列のペアを渡した場合の各メソッドの結果の違いを示しています。  
  
[!code-csharp[DataWorks SqlString_Equals#1](~/../sqlclient/doc/samples/SqlString_Equals.cs#1)]
  
このコードを実行すると、次の出力が生成されます。  
  
```console
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## <a name="next-steps"></a>次のステップ
- [SQL Server のデータ型と ADO.NET](sql-server-data-types.md)