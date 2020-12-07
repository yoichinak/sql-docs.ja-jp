---
description: プロジェクトの設定 (変換) (SybaseToSQL)
title: プロジェクトの設定 (変換) (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/19/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1f4d616b964a1e9e9eed391e3386b16e9df54e44
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195534"
---
# <a name="project-settings-conversion-sybasetosql"></a>プロジェクトの設定 (変換) (SybaseToSQL)

[**プロジェクトの設定**] ダイアログボックスの [**変換**] ページには、Ssma が SAP ADAPTIVE Server Enterprise (ASE) 構文を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL 構文に変換する方法をカスタマイズする設定が含まれています。

[ **変換** ] ペインは、[ **プロジェクトの設定** ] ダイアログボックスと [ **既定のプロジェクトの設定** ] ダイアログボックスで使用できます。

- すべての SSMA プロジェクトの設定を指定する場合は、[ **ツール** ] メニューの [ **既定のプロジェクト設定**] を選択し、左側のウィンドウの下部にある [ **全般** ] をクリックして、[ **変換**] をクリックします。

- 現在のプロジェクトの設定を指定するには、[ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックし、左側のウィンドウの下部にある [ **全般** ] をクリックして、[ **変換**] をクリックします。

## <a name="miscellaneous-section"></a>その他のセクション

### <a name="error"></a>@@ERROR

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL と ASE では、異なるエラーコードが使用されます。

この設定を使用して、ASE コードでへの参照が検出されたときに、SSMA が出力またはエラー一覧ペインに表示するメッセージの種類 (警告またはエラー) を指定し `@@ERROR` ます。

- [変換] を選択し、[ **警告付きでマーク**] を選択すると、ssma はステートメントを変換し、警告コメントでマークします。
- [ **エラー付きでマーク**] を選択した場合、ssma は変換をスキップし、ステートメントにエラーコメントをマークします。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|変換して警告付きでマーク|
|Optimistic|変換して警告付きでマーク|
|完全|エラーでマーク|

### <a name="conversion-of-like-operator"></a>LIKE 演算子の変換

`LIKE`SAP ASE の動作に一致するようにオペランドを変換するかどうかを指定します。 ここで、ASE は、like パターンで末尾の空白をトリムします。 この回避策は、最大有効桁数が指定された固定長データ型に right 式をキャストすることです。
  
- 式を修正せずに変換するには、[ **単純変換** ] を選択します。
- ASE の動作を使用するには、[**固定長にキャスト**] を選択します。
  
[モード] ボックスで変換モードを選択すると、SSMA によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|単純な変換|
|Optimistic|単純な変換|
|完全|固定長にキャスト|

### <a name="convert-or-cast-empty-strings-to-numeric-types"></a>空の文字列を数値型に変換またはキャストする

`CONVERT`または `CAST` 数値型を datatype 引数として使用する式内で、空の文字列または空の文字列を処理する方法を指定します。 この設定では、次のオプションを使用できます。

- 式を修正せずに変換するには、[ **単純変換** ] を選択します。
- **空の文字列を0として**指定した場合、文字列パラメーター `{s}` は式で置き換えられ `CASE ltrim(rtrim({s})) WHEN "" THEN 0 else {s} END` ます。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|単純な変換|
|Optimistic|単純な変換|
|完全|空の文字列がゼロの数値として指定される|

### <a name="concatenation-of-null"></a>NULL の連結

この設定では、文字列の連結をに変換する方法を指定し `NULL` ます。 この特定の設定には、次のオプションを設定できます。

- [ **ISNULL WITH ISNULL function** ] オプションが選択されている場合、連結の非定数はすべてでラップされ、 `string_expression` `ISNULL(string_expression)` `NULL` s は空の文字列に置き換えられます。
- **現在の構文を保持** すると、元の構文が維持されます。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|現在の構文を保持する|
|Optimistic|現在の構文を保持する|
|完全|ISNULL 関数を使用した Wrap|

### <a name="conversion-of-empty-strings"></a>空の文字列の変換

この設定では、空の文字列を変換する方法を指定します。 この特定の設定には、次のオプションを設定できます。

- **すべての文字列式をスペースで置換する**
- **空の文字列定数をスペースで置換する**

Azure SQL の動作を使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **現在の構文を保持**する] を選択します。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|現在の構文を保持する|
|Optimistic|現在の構文を保持する|
|完全|すべての文字列式をスペースで置換する|

### <a name="convert-and-cast-binary-string-conversion"></a>変換し、バイナリ文字列変換をキャストする

バイナリ値を数値に変換すると、異なるプラットフォームで異なる値が返される場合があります。 たとえば、x86 プロセッサでは、 `CONVERT(integer, 0x00000100)` は `65536` ASE でを返しますが、ではを返し `256` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 ASE では、バイトの順序によって異なる値も返されます。

この設定を使用して、SSMA の変換方法 `CONVERT` と `CAST` バイナリ値を含む式を制御します。

- 警告や修正を行わずに式を変換するには、[ **単純変換** ] を選択します。 ASE サーバーにバイナリ値の変更を必要としないバイト順があることがわかっている場合は、この設定を使用します。
- SSMA 変換を行い、で使用する式を修正するには、[ **変換と修正** ] を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 リテラル定数内のバイト順序は逆になります。 その他のバイナリ値 (バイナリ変数や列など) には、エラーが表示されます。 ASE サーバーにバイナリ値の変更を必要とするバイト順があることがわかっている場合は、この値を使用します。

SSMA で式を変換して修正するには、[変換] を選択して [ **警告付き** ] を選択し、変換されたすべての式を警告コメントでマークします。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|変換して警告付きでマーク|
|Optimistic|単純な変換|
|完全|変換と修正|

### <a name="dynamic-sql"></a>動的 SQL

この設定を使用して、ASE コードで動的 SQL が検出されたときに、SSMA が **出力** または **エラー一覧** ペインに表示するメッセージの種類 (警告またはエラー) を指定します。

- [変換] を選択し、 **警告付きでマーク**すると、ssma は動的 SQL を変換し、ステートメントに警告コメントをマークします。
- [ **エラー付きでマーク**] を選択した場合、ssma は変換をスキップし、ステートメントにエラーコメントをマークします。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|変換して警告付きでマーク|
|Optimistic|変換して警告付きでマーク|
|完全|エラーでマーク|

### <a name="equality-check-conversion"></a>等値チェックの変換

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/AZURE sql では、 `ANSI_NULLS` 設定が on の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `UNKNOWN` 等値比較に値が含まれていると、azure sql はを返し `NULL` ます。 `ANSI_NULLS`が off の場合、値を含む等値比較では、 `NULL` 比較対象の列と式、または2つの式の両方が等しい場合に true が返され `NULL` ます。 既定では ( `ANSINULL OFF` )、SAP ASE の等値比較は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL と同じように動作 `ANSI_NULLS OFF` します。

- **単純な変換**を選択した場合、ssma は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 追加の値チェックを行わずに、ASE コードを/Azure SQL 構文に変換し `NULL` ます。 `ANSI_NULLS`が `OFF` Azure SQL である場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはケースごとに等値比較を変更する場合は、この設定を使用します。
- [ **NULL 値を考慮**する] を選択すると、ssma は `NULL` and 句を使用して値のチェックを追加し `IS NULL` `IS NOT NULL` ます。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|単純な変換|
|Optimistic|単純な変換|
|完全|NULL 値を考慮する|

### <a name="format-strings"></a>書式指定文字列

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL では、 `format_string` およびステートメントの引数はサポートされなくなりました `PRINT` `RAISERROR` 。 `format_string`置換可能なパラメーターを文字列に直接格納し、実行時にパラメーターを置き換えることができる引数。 代わりに、で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、文字列リテラルまたは変数を使用して作成された文字列のいずれかを使用して、完全な文字列が必要になります。 詳細については、「 [PRINT ( [!INCLUDE[tsql](../../includes/tsql-md.md)] )](../../t-sql/language-elements/print-transact-sql.md) 」トピックを参照してください。

SSMA が引数を検出すると、 `format_string` 変数を使用して文字列リテラルを作成するか、新しい変数を作成し、その変数を使用して文字列を構築することができます。

- 関数と関数に文字列リテラルを使用するに `PRINT` `RAISERROR` は、[ **新しい文字列の作成**] を選択します。

    このモードでは、PRINT ステートメントまたは RAISERROR ステートメントでプレースホルダーとローカル変数が使用されていない場合、ステートメントは変更されません。 2倍のパーセント文字 (%%)は、PRINT 文字列リテラルで1パーセント文字% に変更されます。

    PRINT ステートメントまたは RAISERROR ステートメントで、次の例のように、プレースホルダーと1つ以上のローカル変数が使用されている場合。

    ```sql
    PRINT 'Total: %1!%%', @percent
    ```

    SSMA は、次の構文に変換します。

    ```sql
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'
    ```

    が変数である場合は `format_string` 、次のステートメントのようになります。  

    ```sql
    PRINT @fmt, @arg1, @arg2
    ```

    SSMA は、単純な文字列変換を行うことはできず、新しい変数を作成する必要があります。

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 =
        REPLACE (@fmt, '%%', '%')
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        CAST (@arg1 AS varchar(max)))
    SET @print_format_1 =
        REPLACE (@print_format_1, '%2!',
        CAST (@arg2 AS varchar(max)))
    PRINT @print_format_1
    ```

    **Create new string** mode を使用する場合、ssma はオプションがであると想定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `CONCAT_NULL_YIELDS_NULL` `OFF` ます。 そのため、SSMA は null 引数をチェックしません。

- SSMA でおよびステートメントごとに新しい変数を作成し、その変数を文字列値として使用するには `PRINT` `RAISERROR` 、[ **新しい変数の作成**] を選択します。

    このモードで `PRINT` は、または `RAISERROR` ステートメントでプレースホルダーとローカル変数が使用されていない場合、ssma は、すべての二重パーセント文字 ( `%%` ) を1パーセント文字で置き換えて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL 構文に従います。

    `PRINT`ステートメントまたは `RAISERROR` ステートメントで、次の例のように、プレースホルダーと1つ以上のローカル変数を使用する場合。

    ```sql
    PRINT 'Total: %1!%%', @percent
    ```

    SSMA は、次の構文に変換します。

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 = 'Total: %1!%'
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))
    PRINT @print_format_1
    ```

    が変数である場合は `format_string` 、次のステートメントのようになります。

    ```sql
    PRINT @fmt, @arg1, @arg2
    ```

    SSMA は、次のように新しい変数を作成し、各引数に null 値があるかどうかをチェックします。

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 =
        REPLACE (@fmt, '%%', '%')
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        ISNULL(CAST (@arg1 AS varchar(max)),''))
    SET @print_format_1 =
        REPLACE (@print_format_1, '%2!',
        ISNULL(CAST (@arg2 AS varchar(max)),''))
    PRINT @print_format_1
    ```

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|新しい文字列の作成|
|Optimistic|新しい文字列の作成|
|完全|新しい変数の作成|

### <a name="insert-an-explicit-value-into-a-timestamp-column"></a>Timestamp 列に明示的な値を挿入する

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL では、timestamp 列への明示的な値の挿入はサポートされていません。

- ステートメントから timestamp 列を除外するに `INSERT` は、[ **列を除外**する] を選択します。
- タイムスタンプ列がステートメントに含まれるたびにエラーメッセージを出力するには `INSERT` 、[ **エラー付きでマーク**] を選択します。 このモードでは、 `INSERT` ステートメントは変換されず、エラーコメントでマークされます。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|列の除外|
|Optimistic|列の除外|
|完全|エラーでマーク|

### <a name="store-temporary-objects-defined-in-procedures"></a>プロシージャで定義されている一時オブジェクトを格納する

この設定は、プロシージャに表示される一時オブジェクトの定義を変換時にソースメタデータに格納するかどうかを指定します。

- メタデータに格納する場合は、[ **はい]** を選択します。
- オブジェクトを保存する必要がない場合は、[ **いいえ** ] を選択します。

|モード|値|
|-|-|
|Default|はい|
|Optimistic|はい|
|完全|いいえ|

### <a name="proxy-table-conversion"></a>プロキシテーブルの変換

ASE プロキシテーブルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AZURE SQL テーブルに変換するか、変換しないかを指定します。また、コードはエラーコメントでマークされます。

- [ **変換** ] を選択して、プロキシテーブルを通常のテーブルに変換します。
- プロキシテーブルコードをエラーコメントでマークするだけの場合は、[ **エラー付きでマーク** ] を選択します。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|エラーでマーク|
|Optimistic|エラーでマーク|
|完全|エラーでマーク|

### <a name="raiserror-base-message-number"></a>RAISERROR base メッセージ番号

ASE ユーザーメッセージは、各データベースに格納されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーメッセージは一元的に格納され、カタログビューで使用できるようになり `sys.messages` ます。 さらに、ASE ユーザーメッセージはで始まり `20000` ますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーメッセージはから始まり `50001` ます。

この設定では、ユーザーメッセージに変換するために ASE ユーザーメッセージ番号に追加する番号を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]カタログビューにユーザーメッセージが含まれている場合は、 `sys.messages` この値を大きくすることが必要になる場合があります。 これは、変換されたメッセージ番号が既存のメッセージ番号と競合しないようにするためです。

次のことを考慮してください。
  
- 範囲内の ASE メッセージ `17000` - `19999` はシステムテーブルからのものであり、変換され `sysmessages` ません。
- ステートメントで参照されているメッセージ番号 `RAISERROR` が定数である場合、SSMA は、新しいユーザーメッセージ番号を決定するために、基本メッセージ番号を定数に追加します。
- 参照されるメッセージ番号が変数または式である場合は、SSMA によって中間のローカル変数が作成されます。
- **オプティミスティックモード**では、ssma は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オプションがであり、 `CONCAT_NULL_YIELDS_NULL` 引数のチェックを行わないことを前提としてい `OFF` `NULL` ます。
- **フルモード**では、ssma は `NULL` 引数をチェックします。
- `RAISERROR` with `arg-list` 引数は変換されません。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|30001|
|Optimistic|30001|
|完全|30001|

### <a name="system-objects"></a>システム オブジェクト

この設定を使用して、ASE システムオブジェクトの使用が検出されたときに [ **出力** ] ペインまたは [ **エラー一覧** ] ペインに表示されるメッセージの種類 (警告またはエラー) を指定します。

- [変換] を選択し、[ **警告付きでマーク**] を選択した場合、ssma は参照をシステムオブジェクトに変換し、警告コメント付きのステートメントをマークします。
- [ **エラー付きでマーク**] を選択した場合、ssma はシステムオブジェクトへの参照を変換せず、ステートメントにエラーコメントをマークします。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|変換して警告付きでマーク|
|Optimistic|変換して警告付きでマーク|
|完全|エラーでマーク|

### <a name="unresolved-identifiers"></a>未解決の識別子

この設定を使用すると、[ **出力** ] ペインまたは [ **エラー一覧** ] ウィンドウで識別子を解決できないときに表示されるメッセージの種類 (警告またはエラー) を指定できます。

- [変換] を選択し、[ **警告付きでマーク**する] を選択すると、ssma は参照を未解決の識別子に変換しようとし、警告コメント付きのステートメントをマークします。
- [ **エラー付きでマーク**] を選択した場合、ssma は参照を未解決の識別子に変換せず、ステートメントにエラーコメントをマークします。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|変換して警告付きでマーク|
|Optimistic|変換して警告付きでマーク|
|完全|エラーでマーク|

## <a name="system-functions-section"></a>システム関数セクション

### <a name="charindex-function"></a>CHARINDEX 関数

ASE で `CHARINDEX` は、 `NULL` すべての入力式がの場合にのみ、を返し `NULL` ます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL は `NULL` 、入力式がの場合にを返し `NULL` ます。

- ASE の動作を使用するには、[ **置換関数**] を選択します。 関数へのすべての呼び出し `CHARINDEX` は、 `CHARINDEX_VARCHAR`  `CHARINDEX_NVARCHAR` `s2ss` SAP ASE の動作をエミュレートするために渡されたパラメーターの型 (スキーマ名の下のユーザーデータベースで作成) に基づいて、またはユーザー定義関数への呼び出しに置き換えられます。
- Azure SQL の動作を使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **現在の構文を保持**する] を選択します。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|現在の構文を保持する|
|Optimistic|現在の構文を保持する|
|完全|Replace 関数|
  
### <a name="datalength-function"></a>DATALENGTH 関数

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL と ASE では、値が単一のスペースである場合、関数によって返される値 `DATALENGTH` が異なります。 この場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL はを返し、ASE はを `0` 返し `1` ます。

- ASE の動作を使用するには、[ **置換関数**] を選択します。 SAP ASE の動作をエミュレートするために、関数へのすべて `DATALENGTH` の呼び出しが式に置き換えられ `CASE` ます。
- 既定の/Azure SQL の動作を使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **現在の構文を保持**する] を選択します。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|現在の構文を保持する|
|Optimistic|現在の構文を保持する|
|完全|Replace 関数|

### <a name="index_col-function"></a>INDEX_COL 関数

ASE では、関数の省略可能な引数をサポートし `user_id` `INDEX_COL` ています。ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL では、この引数はサポートされていません。 引数を使用する場合 `user_id` 、この関数を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL 構文に変換することはできません。

- ASE の動作を使用するには、[ **関数の変換**] を選択します。 コードに引数が含まれている場合は `user_id` 、SSMA によってエラーが表示されます。
- 発生するたびにエラーメッセージを表示するに `INDEX_COL` は、[ **エラー付きでマーク**] を選択します。 SSMA は参照を関数に変換せず、ステートメントにエラーコメントをマークします。

|モード|値|
|-|-|
|Default|エラーでマーク|
|Optimistic|エラーでマーク|
|完全|エラーでマーク|

### <a name="index_colorder-function"></a>INDEX_COLORDER 関数

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL にはシステム関数がありません `INDEX_COLORDER` 。

- ASE の動作を使用するには、[ **関数の変換**] を選択します。 関数へのすべての呼び出し `INDEX_COLORDER` は、 `INDEX_COLORDER` `s2ss` SAP ASE の動作をエミュレートする同じ名前 (スキーマ名の下のユーザーデータベースで作成された) を持つユーザー定義関数の呼び出しに置き換えられます。
- 発生するたびにエラーメッセージを印刷するに `INDEX_COLORDER` は、[ **エラー付きでマーク**] を選択します。 SSMA は参照を関数に変換せず、ステートメントにエラーコメントをマークします。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|エラーでマーク|
|Optimistic|エラーでマーク|
|完全|エラーでマーク|

### <a name="left-and-right-functions"></a>LEFT および RIGHT 関数

`LEFT``RIGHT`ASE の関数と関数は、負の長さのパラメーターに対して異なる動作をします。

- ASE の動作を使用するには、[ **置換関数**] を選択します。 長さのパラメーターは、 `CASE` 負の値を返す式に置き換えられ `NULL` ます。
- SQL Server の動作を使用するには、[ **現在の構文を保持**する] を選択します。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|現在の構文を保持する|
|Optimistic|現在の構文を保持する|
|完全|Replace 関数|

> [!NOTE]
> 長さのパラメーターがリテラル値であり、複雑な式ではない場合、長さの値は常にプロジェクトの設定に関係なく置き換えられ `NULL` ます。

### <a name="next_identity-function"></a>NEXT_IDENTITY 関数

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL にはシステム関数がありません `NEXT_IDENTITY` 。

- ASE の動作を使用するには、[ **関数の変換**] を選択します。 関数へのすべての呼び出し `NEXT_IDENTITY` は `(IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value)` 、SAP ASE の動作をエミュレートする式に置き換えられます。
- 発生するたびにエラーメッセージを印刷するに `NEXT_IDENTITY` は、[ **エラー付きでマーク**] を選択します。 SSMA は参照を関数に変換せず、ステートメントにエラーコメントをマークします。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|エラーでマーク|
|Optimistic|エラーでマーク|
|完全|エラーでマーク|

**既定/オプティミスティック/フルモード:** エラーでマーク

### <a name="patindex-function"></a>PATINDEX 関数

`PATINDEX`関数を SAP ASE の動作に一致するように変換するかどうかを指定します。 ここで、ASE は検索パターンで末尾の空白をトリミングします。 この回避策は、値式を、最大有効桁数を持つ固定長データ型にキャストし、 `rtrim` 関数を検索パターンに適用することです。

- ASE の動作を使用するには、[ **使用**] を選択します。  
- 既定の/Azure SQL の動作を使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **使用しない**] を選択します。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|使用しない|
|Optimistic|使用しない|
|完全|使用|

### <a name="replicate-function"></a>REPLICATE 関数

関数は、 `REPLICATE` 指定された回数だけ文字列を繰り返します。 ASE では、文字列を0回繰り返すように指定した場合、結果はになり `NULL` ます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/AZURE SQL では、結果は空の文字列になります。

- ASE の動作を使用するには、[ **置換関数**] を選択します。 関数へのすべての呼び出し `REPLICATE` は、 `REPLICATE_VARCHAR` `REPLICATE_NVARCHAR` `s2ss` SAP ASE の動作をエミュレートするために渡されたパラメーターの型 (スキーマ名の下のユーザーデータベースで作成) に基づいて、またはユーザー定義関数への呼び出しに置き換えられます。
- 既定の/Azure SQL の動作を使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **置換関数**] を選択します。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|Replace 関数|
|Optimistic|Replace 関数|
|完全|Replace 関数|

### <a name="trim-ltrim-rtrim-function"></a>TRIM (LTRIM, RTRIM) 関数

この設定 `TRIM` では、の呼び出しと、 `LTRIM` `RTRIM` SAP ASE に相当する構文関数または関数を、現在の構文を保持するように置き換えるかどうかを指定します。 この特定の設定には、次のオプションがあります。

- **Replace 関数**
- **現在の構文を保持する**

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|Replace 関数|
|Optimistic|Replace 関数|
|完全|Replace 関数|

### <a name="substring-function"></a>SUBSTRING 関数

ASE では、 `SUBSTRING(expression, start, length)` `NULL` 式の中の文字数よりも大きい値が指定されている場合、または長さが0の場合、関数はを返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/AZURE SQL では、同等の式は空の文字列を返します。

- ASE の動作を使用するには、[ **置換関数**] を選択します。 関数へのすべての呼び出し `SUBSTRING` は、 `SUBSTRING_VARCHAR` `SUBSTRING_NVARCHAR` `SUBSTRING_VARBINARY` `s2ss` SAP ASE の動作をエミュレートするために渡されたパラメーターの型 (スキーマ名の下のユーザーデータベースで作成) に基づいて、またはユーザー定義関数の呼び出しに置き換えられます。
- Azure SQL の動作を使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **現在の構文を保持**する] を選択します。

[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。

|モード|値|
|-|-|
|Default|現在の構文を保持する|
|Optimistic|現在の構文を保持する|
|完全|Replace 関数|

## <a name="tables-section"></a>Tables セクション

### <a name="add-primary-key"></a>主キーの追加

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SAP ASE テーブルに主キーまたは一意のインデックスがない場合は、または AZURE SQL テーブルに新しい主キーを作成します。

|モード|値|
|-|-|
|Default|いいえ|
|Optimistic|いいえ|
|完全|はい|

> [!NOTE]
> Azure SQL に接続している場合、既定では **[はい]** になります。

## <a name="see-also"></a>参照

[ユーザー インターフェイス リファレンス (SybaseToSQL)](../../ssma/sybase/user-interface-reference-sybasetosql.md)
