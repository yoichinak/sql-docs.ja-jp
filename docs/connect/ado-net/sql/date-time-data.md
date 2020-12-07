---
title: 日付型と時刻型のデータ
description: SQL Server 2008 で導入された新しい日付と時刻データ型を使用する方法について説明します。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: ff8e80314210dee9c227360e54f8ba1e6b1a3691
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725653"
---
# <a name="date-and-time-data"></a>日付型と時刻型のデータ

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 2008 では、日付と時刻の情報を処理するための新しいデータ型が導入されています。 新しいデータ型には、日付と時刻の個別の型と、より大きな範囲、精度、およびタイムゾーンに対応する拡張データ型が含まれます。 Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) では、SQL Server 2008 データベース エンジンのすべての新機能を完全にサポートしています。 SqlClient でこれらの新機能を使用するには、.NET Framework 3.5 SP1 (またはそれ以降) または .NET Core 1.0 (またはそれ以降) をインストールする必要があります。  
  
SQL Server 2008 より前のバージョンの SQL Server では、日付と時刻の値を操作するために 2 つのデータ型 (`datetime` と `smalldatetime`) しかありませんでした。 いずれのデータ型も日付値と時刻値の両方を保持するため、日付と時刻のどちらか一方の値のみを使用する場合にはかえって面倒になります。 さらに、これらのデータ型では、1753 年に英国でグレゴリオ暦が導入された後の日付のみがサポートされます。 もう 1 つの制限事項は、これらの古いデータ型がタイムゾーンに対応していないことです。これにより、複数のタイムゾーンからのデータの操作が困難になります。  
  
SQL Server のデータ型の詳細なドキュメントについては SQL Server オンライン ブックを参照してください。 日付型と時刻型のデータに関するエントリレベルのトピックについては、「[日時データの使用](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))」を参照してください。
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>SQL Server 2008 で導入された日付/時刻データ型  
 次の表では、新しい新しい日付と時刻のデータ型について説明します。  
  
|SQL Server のデータ型|説明|  
|--------------------------|-----------------|  
|`date`|`date` データ型は、01 年 1 月 1 日から 9999 年 12 月 31 日の範囲を 1 日の精度で表すことができます。 既定値は 1900 年 1 月 1 日です。 ストレージ サイズは 3 バイトです。|  
|`time`|`time` データ型は、24 時間形式で時刻値のみを格納します。 `time` データ型は、00:00:00.0000000 から 23:59:59.9999999 の範囲で、100 ナノ秒の精度です。 既定値は 00:00: 00.0000000 (午前 0 時) です。 `time` データ型はユーザー定義による 1 秒未満の時間の有効桁数をサポートし、記憶領域のサイズは、指定された有効桁数に応じて 3 バイトから 6 バイトまでになります。|  
|`datetime2`|`datetime2` データ型では、`date` データ型と `time` データ型の範囲と精度が 1 つのデータ型に結合されます。<br /><br /> 既定値と文字列リテラルの形式は、`date` データ型および `time` データ型で定義されているものと同じです。|  
|`datetimeoffset`|`datetimeoffset` データ型は、`datetime2` のすべての機能に加えて、タイム ゾーン オフセットを持ちます。 タイム ゾーン オフセットは、[+&#124;-] HH:MM として表されます。 HH は、タイム ゾーン オフセットの時間数を表す 00 から 14 までの 2 桁の数字です。 MM は、タイム ゾーン オフセットの付加的な分数を表す 00 から 59 までの 2 桁の数字です。 時刻形式の精度は 100 ナノ秒までサポートされています。 必須の + または - 記号は、ローカル時刻を取得するために、UTC (協定世界時またはグリニッジ標準時) からタイム ゾーン オフセットを加算するか減算するかを示します。|  
  
> [!NOTE]
>  `Type System Version` キーワードの詳細については、「<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。  
  
## <a name="date-format-and-date-order"></a>日付の形式と日付の順序  
SQL Server で日付と時刻の値を解析する方法は、型システムのバージョンとサーバーのバージョンだけでなく、サーバーの既定の言語と形式の設定にも依存します。 ある言語の日付形式に対して機能する日付文字列は、別の言語および日付形式の設定を使用する接続によってクエリが実行された場合に認識されない可能性があります。  
  
Transact-SQL SET LANGUAGE ステートメントでは、日付部分の順序を決定する DATEFORMAT を暗黙的に設定します。 接続に対して SET DATEFORMAT Transact-SQL ステートメントを使用して、MDY、DMY、YMD、YDM、MYD、DYM の順序で日付部分を並べ替えることにより、日付値を明確にすることができます。  
  
接続に対して DATEFORMAT を指定しない場合、SQL Server では接続に関連付けられている既定の言語が使用されます。 たとえば、' 01/02/03' の日付文字列は、米国英語の言語設定のサーバーでは MDY (2003 年 1 月 2 日) として解釈され、英国英語の言語設定のサーバーでは DMY (2003 年 2 月 1 日) として解釈されます。 年は SQL Server の終了年のルールを使用して決定されます。このルールでは、世紀値を割り当てるための終了日を定義しています。 詳細については、SQL Server オンライン ブックの「[two digit year cutoff オプション](/previous-versions/sql/sql-server-2008-r2/ms189577(v=sql.105))」を参照してください。  
  
> [!NOTE]
>  文字列形式から `date`、`time`、`datetime2`、または `datetimeoffset` に変換する場合、YDM 日付形式はサポートされていません。  
  
SQL Server で日付と時刻のデータがどのように解釈されるかの詳細については、SQL Server 2008 オンライン ブックの「[日時データの使用](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))」を参照してください。  
  
## <a name="datetime-data-types-and-parameters"></a>日付/時刻データ型とパラメーター  
新しい日付と時刻のデータ型をサポートするため、<xref:System.Data.SqlDbType> に次の列挙値が追加されています。  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

<xref:Microsoft.Data.SqlClient.SqlParameter> のデータ型は、前の <xref:System.Data.SqlDbType> 列挙型のいずれかの値を使って指定できます。 

> [!NOTE]
> `DbType` の `SqlParameter` プロパティは `SqlDbType.Date` に設定できません。

<xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> プロパティを特定の `SqlParameter` に設定することで、汎用的に <xref:System.Data.DbType> の型を指定することもできます。 <xref:System.Data.DbType> 型と `datetime2` 型をサポートするため、`datetimeoffset` には、次の列挙値が追加されています。  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
これらの新しい列挙型は、`Date`、`Time`、および `DateTime` 列挙型を補完します。  
  
パラメーター オブジェクトの Microsoft SqlClient Data Provider 型は、パラメーター オブジェクトの値の .NET 型、またはパラメーター オブジェクトの `DbType` から推論されます。 新しい日付と時刻のデータ型をサポートするための新しい <xref:System.Data.SqlTypes> データ型は導入されていません。 次の表に、SQL Server 2008 の日付と時刻のデータ型と CLR データ型のマッピングについて説明します。  
  
|SQL Server のデータ型|.NET の種類|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|date|System.DateTime|Date|Date|  
|time|System.TimeSpan|Time|Time|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|DATETIME|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>SqlParameter のプロパティ  
 次の表に、日付と時刻のデータ型に関連する `SqlParameter` のプロパティについて説明します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|値が null 許容であるかどうかを取得または設定します。 サーバーに null パラメーター値を送信する場合、<xref:System.DBNull> (Visual Basic では `null`) ではなく、`Nothing` を指定する必要があります。 データベースの null 値の詳細については、「[null 値の処理](handle-null-values.md)」を参照してください。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|値を表すために使用される最大桁数を取得または設定します。 この設定は日付と時刻のデータ型では無視されます。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|小数点以下の桁数を取得または設定します。これは `Time`、`DateTime2`、`DateTimeOffset` の時刻部分の値の処理で使用されます。 既定値は 0 で、これは実際のスケールが値から推論され、サーバーに送信されることを意味します。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|日付と時刻のデータ型では無視されます。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|パラメーター値を取得または設定します。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|パラメーター値を取得または設定します。|  
  
> [!NOTE]
>  0 時未満または 24 時以上の時刻値では、<xref:System.ArgumentException> がスローされます。  
  
### <a name="creating-parameters"></a>パラメーターの作成  
<xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトを作成するには、そのコンストラクターを使用するか、それを <xref:Microsoft.Data.SqlClient.SqlCommand>.<xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> コレクションに、`Add` の <xref:Microsoft.Data.SqlClient.SqlParameterCollection> メソッドを呼び出すことによって追加します。 `Add` メソッドは、コンストラクター引数または既存のパラメーター オブジェクトのいずれかを入力として受け取ります。  
  
このトピックの次のセクションでは、日付と時刻のパラメーターを指定する方法の例について説明します。
  
### <a name="date-example"></a>日付の例  
次のコード フラグメントでは、`date` パラメーターを指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>時刻の例  
次のコード フラグメントでは、`time` パラメーターを指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Datetime2 の例  
次のコード フラグメントでは、日付部分と時刻部分の両方を含む `datetime2` パラメーターを指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>DateTimeOffSet の例  
次のコード フラグメントでは、日付、時刻、およびタイム ゾーン オフセットが 0 の `DateTimeOffSet` パラメーターを指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
次のコード フラグメントに示すように、`AddWithValue` の <xref:Microsoft.Data.SqlClient.SqlCommand> メソッドを使用してパラメーターを指定することもできます。 ただし、`AddWithValue` メソッドでは、パラメーターの <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> または <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> を指定することはできません。  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
`@date` パラメーターは、サーバー上の `date`、`datetime`、または `datetime2` データ型にマッピングできます。 新しい `datetime` データ型を使用する場合は、パラメーターの <xref:System.Data.SqlDbType> プロパティをインスタンスのデータ型に明示的に設定する必要があります。 <xref:System.Data.SqlDbType.Variant> を使用するか、または暗黙的にパラメーター値を指定すると、`datetime` データ型および `smalldatetime` データ型との下位互換性の問題が発生する可能性があります。  
  
次の表は、どの CLR 型からどの `SqlDbTypes` が推論されるかを示しています。  
  
|CLR 型|推定される SqlDbType|  
|--------------|------------------------|  
|DateTime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>日付と時刻のデータの取得  
SQL Server 2008 の date 値と time 値を取得するためのメソッドを次の表に示します。  
  
|SqlClient のメソッド|説明|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|指定された列の値を <xref:System.DateTime> 構造体として取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|指定された列の値を <xref:System.DateTimeOffset> 構造体として取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|そのフィールドの基になるプロバイダー固有の型である型を返します。 新しい日付と時刻の型に対して `GetFieldType` と同じ型を返します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|指定した列の値を取得します。 新しい日付と時刻の型に対して `GetValue` と同じ型を返します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|指定した配列内の値を取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|列の値を <xref:System.Data.SqlTypes.SqlString> として取得します。 データを <xref:System.InvalidCastException> として表現できない場合、`SqlString` が発生します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|列データをその既定の `SqlDbType` として取得します。 新しい日付と時刻の型に対して `GetValue` と同じ型を返します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|指定した配列内の値を取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|Type System Version が SQL Server 2005 に設定されている場合、列の値を文字列として取得します。 データを文字列として表現できない場合、<xref:System.InvalidCastException> が発生します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|指定された列の値を <xref:System.TimeSpan> 構造体として取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|指定した列の値を、その基になる CLR 型として取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|配列内の列の値を取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|結果セットのメタデータを記述する <xref:System.Data.DataTable> を返します。|  
  
> [!NOTE]
>  新しい日付と時刻の `SqlDbTypes` は、SQL Server でインプロセスで実行されているコードではサポートされていません。 これらの型のいずれかがサーバーに渡されると、例外が発生します。  
  
## <a name="specifying-date-and-time-values-as-literals"></a>日付と時刻の値をリテラルとして指定する  
日付と時刻のデータ型は、さまざまなリテラル文字列形式を使用して指定できます。SQL Server で実行時にそれが評価され、内部の日付/時刻構造に変換されます。 SQL Server では、一重引用符 (') で囲まれた日付と時刻のデータが認識されます。 次の例に、いくつかの形式を示します。  
  
- アルファベットの日付形式 (`'October 15, 2006'` など)。  
  
- 数値の日付形式 (`'10/15/2006'`など)。  
  
- 区切られていない文字列形式 (`'20061015'` など。これは ISO 標準日付形式を使用している場合、2006 年 10 月 15 日と解釈される)。  
  
> [!NOTE]
>  すべてのリテラル文字列形式と、日付と時刻のデータ型のその他の機能に関する完全なドキュメントについては、SQL Server オンライン ブックを参照してください。  
  
0 時未満または 24 時以上の時刻値では、<xref:System.ArgumentException> がスローされます。  
  
## <a name="resources-in-sql-server-2008-books-online"></a>SQL Server 2008 オンラインブックのリソース  
SQL Server 2008 での日付と時刻の値の操作の詳細については、SQL Server 2008 オンライン ブックの次の情報を参照してください。  
  
|トピック|説明|  
|-----------|-----------------|  
|[日付と時刻のデータ型および関数 (Transact-SQL)](/previous-versions/sql/sql-server-2008/ms186724(v=sql.100))|Transact-SQL の日付と時刻のデータ型と関数の概要を説明します。|  
|[日時データの使用](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))|日付と時刻のデータ型と関数に関する情報とそれらの使用例を提供します。|  
|[データ型 (Transact-SQL)](/previous-versions/sql/sql-server-2008/ms187752(v=sql.100))|SQL Server 2008 のシステム データ型について説明します。|  
  
## <a name="next-steps"></a>次のステップ
- [SQL Server のデータ型と ADO.NET](sql-server-data-types.md)