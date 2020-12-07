---
description: '[高度な編集] (条件) ダイアログ ボックス'
title: '[高度な編集] (条件) ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.condition.advancededit.f1
ms.assetid: a0bbe501-78c5-45ad-9087-965d04855663
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 60664db09d71d0ec6a9049a568af057ffea84a6c
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127933"
---
# <a name="advanced-edit-condition-dialog-box"></a>[高度な編集] (条件) ダイアログ ボックス
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **[高度な編集]** ダイアログ ボックスでは、ポリシー ベースの管理条件に使用する複雑な式を作成できます。  
  
## <a name="options"></a>オプション  
 **[セル値]**  
 セル値に使用するために作成した関数または式が表示されます。 **[OK]** をクリックすると、 **[新しい条件の作成]** ダイアログ ボックスまたは **[条件を開く]** ダイアログ ボックスの **[全般]** ページにある条件式ボックスの **[フィールド]** セルまたは **[値]** セルにセル値が表示されます。  
  
 **[関数とプロパティ]**  
 使用可能な関数とプロパティが表示されます。  
  
 **詳細**  
 関数とプロパティに関する情報として、関数シグネチャ、関数の説明、戻り値、例が表示されます。  
  
## <a name="syntax"></a>構文  
 有効な式は次の形式にする必要があります。  
  
 `{property | function | constant}`  
  
 `{operator}`  
  
 `{property | function | constant}`  
  
## <a name="examples"></a>例  
 有効な式の例を以下に示します。  
  
-   *Property1*> 5  
  
-   *Property1*=*Property2*  
  
-   Add(5, Multiply(.2,*Property1*))<*Property2*  
  
-   *Sometext* IN *Property1*  
  
-   *Property1*< Fn(*Property2*)  
  
-   BitwiseAnd(*Property1*,*Property2*)= 0  
  
## <a name="additional-function-information"></a>関数に関する追加情報  
 以下のセクションでは、ポリシー ベースの管理条件のための複雑な式の作成に使用できる関数に関する追加情報を提供します。  
  
> **重要:** ポリシー ベースの管理条件の作成に使用できる関数は、必ずしも [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を使用しません。 例に示されている構文に必ず従ってください。 たとえば、 **DateAdd** 関数または **DatePart** 関数を使用する場合は、 *datepart* 引数を単一引用符で囲む必要があります。  
  
|機能|署名|説明|引数|戻り値|例|  
|--------------|---------------|-----------------|---------------|------------------|-------------|  
|**Add()**|Numeric Add (Numeric *expression1*, Numeric *expression2*)|2 つの値を加算します。|*expression1* および *expression2* - **bit** データ型を除く、数値カテゴリのデータ型のいずれかに属する任意の有効な式です。 定数、プロパティ、または数値型を返す関数を指定できます。|最も優先順位の高い引数のデータ型を返します。|`Add(Property1, 5)`|  
|**Array()**|Array Array (VarArgs *expression*)|値のリストから配列を作成します。 Sum() や Count() などの集計関数で使用できます。|*expression* - 配列に変換される式です。|配列|`Array(2,3,4,5,6)`|  
|**Avg()**|Numeric Avg (*VarArgs*)|引数リスト内の値の平均を返します。|*VarArgs* - **bit** データ型を除く、真数または概数のデータ型カテゴリに属するバリアント型の式のリストです。|戻り値の型は、式の評価された結果の型によって決定されます。<br /><br /> 式の結果が **integer**、 **decimal**、 **money** / **smallmoney**、および **float** / **real** カテゴリである場合は、戻り値の型はそれぞれ **int**、 **decimal**、 **money**、および **float** になります。|`Avg(1.0, 2.0, 3.0, 4.0, 5.0)` は `3.0` を返します。|  
|**BitwiseAnd()**|Numeric BitwiseAnd (Numeric *expression 1*, Numeric *expression2*)|2 つの整数値の間でビットごとの論理積演算を実行します。|*expression1* および *expression2* - 整数のデータ型カテゴリのいずれかのデータ型に属する任意の有効な式です。|整数のデータ型カテゴリの値を返します。|`BitwiseAnd(Property1, Property2)`|  
|**BitwiseOr()**|Numeric BitwiseOr (Numeric *expression1*, Numeric *expression2*)|指定された 2 つの整数値間でビットごとの論理 OR 演算を実行します。|*expression1* および *expression2* - 整数のデータ型カテゴリのいずれかのデータ型に属する任意の有効な式です。|整数のデータ型カテゴリの値を返します。|`BitwiseOr(Property1, Property2)`|  
|**Concatenate()**|String Concatenate (String *string1*, String *string2*)|2 つの文字列を連結します。|*string1* および *string2* - 連結する 2 つの文字列です。 NULL 以外の任意の有効な文字列を指定できます。|*string1* の後に *string2* を連結した文字列。|`Concatenate("Hello", " World` `")` は、"`Hello World`" を返します。|  
|**Count()**|Numeric Count (*VarArgs*)|引数リスト内の項目数を返します。|*VarArgs* - **text**、 **image**、 **ntext** を除く、任意の型の式です。|整数のデータ型カテゴリの値を返します。|`Count(1.0, 2.0, 3.0, 4.0, 5.0)` は `5` を返します。|  
|**DateAdd()**|DateTime DateAdd (String *datepart*, Numeric *number*, DateTime *date*)|指定された日付に期間を加えた新しい **datetime** の値を返します。|*datepart* - 新しい値を返す日付の要素を指定するパラメーターです。 year(yy, yyyy)、month(mm, m)、dayofyear(dy, y) などの型がサポートされています。 詳細については、「[DATEADD &#40;Transact-SQL&#41;](../../t-sql/functions/dateadd-transact-sql.md)」を参照してください。<br /><br /> *number* - *datepart* に加算される値です。<br /><br /> *date* - **datetime** 型の値を返す式、または日付形式の文字列です。|指定された日付に期間を加えた新しい **datetime** の値です。|**例:** `DateAdd('day', 21, DateTime('2007-08-06 14:21:50'))` は `'2007-08-27 14:21:50'` を返します。<br /><br /> この関数でサポートされている *dateparts* とその省略形は、次のとおりです。<br /><br /> **year**: yy, yyyy<br /><br /> **month**: mm, m<br /><br /> **dayofyear**: dy, y<br /><br /> **day**: dd, d<br /><br /> **week**: wk, ww<br /><br /> **weekday**: dw, w<br /><br /> **hour**: hh<br /><br /> **minute**: mi, n<br /><br /> **second**: ss, s<br /><br /> **millisecond**: ms|  
|**DatePart()**|Numeric DatePart (String *datepart*, DateTime *date*)|指定された日付の特定の *datepart* を表す整数を返します。|*datepart* - 返す対象となる日付要素を指定するパラメーターです。 year(yy, yyyy)、month(mm, m)、dayofyear(dy, y) などの型がサポートされています。 詳細については、「[DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)」を参照してください。<br /><br /> *date* - **datetime** 型の値を返す式、または日付形式の文字列です。|指定された日付の特定の *datepart* を表す、整数のデータ型カテゴリの値を返します。|`DatePart('month', DateTime('2007-08-06 14:21:50.620'))` は `8` を返します。|  
|**DateTime()**|DateTime DateTime (String *dateString*)|文字列から datetime 値を作成します。|*dateString* - 文字列としての datetime 値です。|入力文字列から作成された datetime 値を返します。|`DateTime('3/12/2006')`|  
|**Divide()**|Numeric Divide (Numeric *expression_dividend*, Numeric *expression_divisor*)|1 つの値を別の値で除算します。|*expression_dividend* - 除算される数値式です。 被除数には、数値型に分類されるデータ型を持つ有効な式を指定できます。ただし、 **datetime** データ型は除きます。<br /><br /> *expression_divisor* - 被除数を除算する数値式です。 除数には、数値型に分類されるデータ型を持つ有効な式を指定できます。ただし、 **datetime** データ型は除きます。|最も優先順位の高い引数のデータ型を返します。|**例:** `Divide(Property1, 2)`<br /><br /> 注: これは double 型の演算になります。 整数との比較を行う場合は、 `Round()`で結果を結合する必要があります。 (例: `Round(Divide(10, 3), 0) = 3`)。|  
|**Enum()**|Numeric Enum (String *enumTypeName*, String *enumValueName*)|文字列から列挙値を作成します。|*enumTypeName* - 列挙型の名前です。<br /><br /> *enumValueName* - 列挙の値です。|列挙値を数値として返します。|`Enum('CompatibilityLevel','Version100')`|  
|**Escape()**|String Escape (String *replaceString*, String *stringToEscape*, String *escapeString*)|指定したエスケープ文字列で入力文字列のサブストリングをエスケープします。|*replaceString* - 入力文字列です。<br /><br /> *stringToEscape* - *replaceString* のサブストリングです。 この文字列の前にエスケープ文字列が追加されます。<br /><br /> *escapeString* - *stringToEscape* の各インスタンスの前に追加するエスケープ文字列です。|*stringToEscape* の各インスタンスの前に *escapeString* が付いた変更後の *replaceString* を返します。|`Escape("Hello", "l", "[")` は、"`He[l[lo`" を返します。|  
|**ExecuteSQL()**|Variant ExecuteSQL (String *returnType*, String *sqlQuery*)|ターゲット サーバーに対して [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを実行します。<br /><br /> ExecuteSql() の詳細については、「 [ExecuteSql()](/archive/blogs/sqlpbm/executesql)」を参照してください。|*returnType* - [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントによって返されるデータの型を指定します。 *returnType* の有効なリテラルは、 **Numeric**、 **String**、 **Bool**、 **DateTime**、 **Array**、および **Guid** です。<br /><br /> *sqlQuery* - 実行するクエリを格納する文字列です。||`ExecuteSQL ('Numeric', 'SELECT COUNT(*) FROM msdb.dbo.sysjobs') <> 0`<br /><br /> SQL Server のターゲット インスタンスに対して、スカラー値 Transact-SQL クエリを実行します。 `SELECT` ステートメントでは 1 列のみ指定できます。その列より後の列は無視されます。 実行されるクエリでは 1 行のみ返されることが必要です。その行より後の行は無視されます。 クエリから空のセットが返される場合、 `ExecuteSQL` に基づいて作成される条件式は false と評価されます。 `ExecuteSql` では、 **[要求時]** および **[スケジュールで実行]** 評価モードがサポートされます。<br /><br /> -`@@ObjectName`:<br />                      [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)の名前フィールドに対応します。 変数は、現在のオブジェクトの名前に置き換えられます。<br /><br /> -`@@SchemaName`: [sys.schemas](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md) の名前フィールドに対応します。 変数は、現在のオブジェクトのスキーマ名に置き換えられます (該当する場合)。<br /><br /> 注: ExecuteSQL ステートメントに単一引用符を含めるには、もう 1 つ単一引用符を使用して元の単一引用符をエスケープします。 たとえば、O'Brian というユーザー名への参照を含める場合は、「O''Brian」と入力します。|  
|**ExecuteWQL()**|Variant ExecuteWQL (string *returnType* , string *namespace*, string *wql*)|指定された名前空間に対して WQL スクリプトを実行します。 SELECT ステートメントには、戻り値の列を 1 つだけ含めることができます。 複数の列を指定すると、エラーがスローされます。|*returnType* - WQL によって返されるデータの型を指定します。 有効なリテラルは、 **Numeric**、 **String**、 **Bool**、 **DateTime**、 **Array**、および **Guid** です。<br /><br /> *namespace* - 実行対象の WMI 名前空間です。<br /><br /> *wql* - 実行する WQL を格納する文字列です。||`ExecuteWQL('Numeric', 'root\CIMV2', 'select NumberOfProcessors from win32_ComputerSystem') <> 0`|  
|**False()**|Bool False()|ブール値 FALSE を返します。|なし|ブール値 FALSE を返します。|`IsDatabaseMailEnabled = False()`|  
|**GetDate()**|DateTime GetDate()|システム日付を返します。|なし|システム日付を DateTime として返します。|`@DateLastModified = GetDate()`|  
|**Guid()**|Guid Guid(String *guidString*)|文字列から GUID を返します。|*guidString* - 作成される GUID の文字列表記です。|文字列から作成された GUID を返します。|`Guid('12340000-0000-3455-0000-000000000454')`|  
|**IsNull()**|Variant IsNull (Variant *check_expression*, Variant *replacement_value*)|*check_expression* の値が NULL でない場合、その値が返されます。それ以外の場合は、 *replacement_value* が返されます。 型が異なる場合、 *replacement_value* は *check_expression* の型に暗黙的に変換されます。|*check_expression* - NULL かどうかを調べる式です。 *check_expression* には、ポリシー ベースの管理でサポートされる型 (Numeric、String、Bool、DateTime、Array、および Guid) を指定できます。<br /><br /> *replacement_value* - *check_expression* が NULL の場合に返される式です。 *replacement_value* は、暗黙的に *check_expression* の型に変換される型である必要があります。|戻り値の型は、 *check_expression* が NULL 以外の場合は *check_expression* の型です。それ以外の場合は *replacement_value* の型が返されます。||  
|**Len()**|Numeric Len (*string_expression*)|指定された文字列式の文字数 (末尾の空白文字を除く) を返します。|*string_expression* - 評価する文字列式です。|整数のデータ型カテゴリの値を返します。|`Len('Hello')` は `5` を返します。|  
|**Lower()**|String Lower (String *_expression*)|文字列の大文字をすべて小文字に変換して返します。|*expression* - 変換対象の文字列式です。|大文字をすべて小文字に変換した後のソース文字列式を表す文字列を返します。|`Len('HeLlO')` は `'hello'` を返します。|  
|**Mod()**|Numeric Mod (Numeric *expression_dividend*, Numeric *expression_divisor*)|最初の数値式を 2 番目の数値式で割った剰余を整数値で返します。|*expression_dividend* - 除算される数値式です。 *expression_dividend* には、整数または数値に分類されるデータ型の有効な式を指定する必要があります。<br /><br /> *expression_divisor* - 被除数を除算する数値式です。 *expression_divisor* には、整数または数値に分類されるデータ型の有効な式を指定する必要があります。|整数のデータ型カテゴリの値を返します。|`Mod(Property1, 3)`|  
|**Multiply()**|Numeric Multiply (Numeric *expression1*, Numeric *expression2*)|2 つの式を乗算します。|*expression1* および *expression2* - **datetime** データ型を除く、数値カテゴリのデータ型のいずれかに属する任意の有効な式です。|最も優先順位の高い引数のデータ型を返します。|`Multiply(Property1, .20)`|  
|**Power()**|Numeric Power (Numeric *numeric_expression*, Numeric *expression_power*)|指定されたべき乗の指定された式の値を返します。|*numeric_expression* - bit データ型を除く、真数データ型または概数データ型の式です。<br /><br /> *expression_power* - *numeric_expression* のべき乗値です。 *expression_power* には、 **bit** データ型を除く、真数または概数のデータ型カテゴリの式を指定できます。|戻り値の型は *numeric_expression* と同じです。|`Power(Property1, 3)`|  
|**Round()**|Numeric Round (Numeric *expression*, Numeric *expression_precision*)|指定された長さまたは有効桁数に丸めた数値式を返します。|*expression* - **bit** データ型を除く、真数データ型または概数データ型の式です。<br /><br /> *expression_precision* - 式の丸め結果とする有効桁数です。 *expression_precision* に正の値を指定した場合、 *numeric_expression* は length で指定した小数点以下桁数に丸められます。 *expression_precision* に負の値を指定した場合、 *numeric_expression* は *expression_precision* で指定した小数点の左側の位置で丸められます。|*numeric_expression* と同じ型を返します。|`Round(5.333, 0)`|  
|**String()**|String String (Variant *_expression*)|バリアントを文字列に変換します。|*expression* - 文字列に変換するバリアントの式です。|バリアントの式の文字列値を返します。|`String(4)`|  
|**Sum()**|Numeric Sum (*VarArgs*)|引数リスト内のすべての値の合計を返します。 Sum は、数値と共に使用できます。|*VarArgs*- **bit** データ型を除く、真数または概数のデータ型カテゴリに属するバリアント型の式のリストです。|最も正確な式のデータ型ですべての式の値の合計を返します。<br /><br /> 式の結果が **integer**、 **numeric**、 **money** / **small money**、および **float** / **real** カテゴリである場合は、戻り値の型はそれぞれ **int**、 **numeric**、 **money**、および **float** になります。|`Sum(1.0, 2.0, 3.0, 4.0, 5.0)` は `15` を返します。|  
|**True()**|Bool TRUE()|ブール値 TRUE を返します。||ブール値 TRUE を返します。|`IsDatabaseMailEnabled = True()`|  
|**Upper()**|String Upper (String *_expression*)|文字列の小文字をすべて大文字に変換して返します。|*expression* - 変換対象の文字列式です。|小文字をすべて大文字に変換した後のソース文字列式を表す文字列を返します。|`Upper('HeLlO')` は `'HELLO'` を返します。|  
  
## <a name="see-also"></a>関連項目  
 [[新しい条件の作成] または [条件を開く] ダイアログ ボックスの [全般] ページ](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md)   
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
