---
description: CREATE TABLE - SQL コマンド
title: CREATE TABLE-SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ea84b28e12194ffb1a1b181089622cd169c91b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471634"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL コマンド
指定されたフィールドを含むテーブルを作成します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブな Visual FoxPro 言語構文がサポートされています。 ドライバー固有の情報については、「 **ドライバーの解説**」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>引数  
 CREATE TABLE &#124; DBF *TableName1*  
 作成するテーブルの名前を指定します。 TABLE オプションと DBF オプションは同じです。  
  
 名前 *Longtablename*  
 テーブルの長い名前を指定します。 長いテーブル名は、データベースが開いている場合にのみ指定できます。これは、長いテーブル名がデータベースに格納されるためです。  
  
 長い名前には、最大128文字を含めることができ、データベース内の短いファイル名の代わりに使用できます。  
  
 FREE  
 開いているデータベースにテーブルが追加されないように指定します。 データベースが開いていない場合、FREE は不要です。  
  
 *(FieldName1 FieldType* [( *nfieldwidth* [, *nprecision*])]  
 フィールド名、フィールドの種類、フィールドの幅、およびフィールドの有効桁数 (小数点以下桁数) をそれぞれ指定します。  
  
 *FieldType* は、フィールドの [データ型](../../odbc/microsoft/visual-foxpro-field-data-types.md)を示す単一の文字です。 一部のフィールドデータ型では、 *Nfieldwidth* または *nprecision* またはその両方を指定する必要があります。  
  
 *Nfieldwidth* と *Nprecision* は、D、G、I、L、M、P、T、および Y 型では無視されます。 n precision が B、F、N のいずれの型にも含まれ*ていない場合、* *nprecision*の既定値は 0 (小数点以下の桁数ではありません) になります。  
  
 NULL  
 フィールドの null 値を許可します。  
  
 NOT NULL  
 フィールドの null 値を回避します。  
  
 Null と NOT NULL を省略すると、SET NULL の現在の設定によって、フィールドで null 値が許可されるかどうかが決まります。 ただし、null および NOT NULL を省略し、PRIMARY KEY または UNIQUE 句を含めると、SET NULL の現在の設定は無視され、フィールドの既定値は NULL になりません。  
  
 *LExpression1*の確認  
 フィールドの検証規則を指定します。 *lExpression1* ユーザー定義関数を指定できます。 空白のレコードが追加されるたびに、検証規則がチェックされます。 追加されたレコードで空のフィールド値が検証規則によって許可されていない場合、エラーが生成されます。  
  
 エラー *cMessageText1*  
 フィールド規則によってエラーが生成された場合に表示されるエラーメッセージを指定します。 このメッセージは、[参照] ウィンドウまたは編集ウィンドウ内でデータが変更された場合にのみ表示されます。  
  
 既定の *eExpression1*  
 フィールドの既定値を指定します。 *EExpression1*のデータ型は、フィールドのデータ型と同じである必要があります。  
  
 PRIMARY KEY  
 フィールドのプライマリインデックスを作成します。 プライマリインデックスタグには、フィールドと同じ名前が付けられています。  
  
 UNIQUE  
 フィールドの候補インデックスを作成します。 候補インデックスタグには、フィールドと同じ名前が付けられています。  
  
> [!NOTE]  
>  候補インデックス (CREATE TABLE または ALTER TABLE-SQL に UNIQUE オプションを含めることによって作成されたもの) は、INDEX コマンドで UNIQUE オプションを使用して作成されたインデックスと同じではありません。 Index コマンドで UNIQUE オプションを使用して作成されたインデックスでは、重複するインデックスキーが許可されます。候補インデックスでは、重複するインデックスキーは許可されません。 一意のオプションの詳細については、「 [INDEX](../../odbc/microsoft/index-command.md) 」を参照してください。  
  
 プライマリまたは候補のインデックスに使用されるフィールドでは、Null 値と重複レコードは許可されません。 ただし、null 値をサポートするフィールドのプライマリインデックスまたは候補インデックスを作成した場合、Visual FoxPro ではエラーは生成されません。 プライマリまたは候補のインデックスに使用するフィールドに null 値または重複値を入力しようとすると、Visual FoxPro でエラーが発生します。  
  
 *TableName2*の参照 [TAG *TagName1*]  
 永続的なリレーションシップを確立する親テーブルを指定します。 タグ *TagName1*を省略した場合、リレーションシップは親テーブルのプライマリインデックスキーを使用して確立されます。 親テーブルにプライマリインデックスがない場合、Visual FoxPro ではエラーが生成されます。  
  
 親テーブルの既存のインデックスタグに基づいてリレーションシップを確立するには、タグ *TagName1* を含めます。 インデックスタグ名には、最大10文字まで含めることができます。  
  
 親テーブルをフリーテーブルにすることはできません。  
  
 NOCPTRANS  
 文字フィールドとメモフィールドの別のコードページに変換できないようにします。 テーブルを別のコードページに変換した場合、NOCPTRANS が指定されているフィールドは翻訳されません。 NOCPTRANS は、文字フィールドとメモフィールドに対してのみ指定できます。  
  
 次の例では、2つの文字フィールドと2つのメモフィールドを含む mytable という名前のテーブルを作成します。 2番目の文字フィールド、char2、および2番目のメモフィールド memo2 には、変換を防止するための NOCPTRANS が含まれています。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主キー *eExpression2* タグ *TagName2*  
 作成するプライマリインデックスを指定します。 *eExpression2* は、テーブル内のフィールドまたはフィールドの組み合わせを指定します。 タグ *TagName2* 作成されるプライマリインデックスタグの名前を指定します。 インデックスタグ名には、最大10文字まで含めることができます。  
  
 テーブルで使用できるプライマリインデックスは1つだけなので、フィールドのプライマリインデックスを既に作成している場合は、この句を含めることはできません。 CREATE TABLE に複数の主キー句を含めると、Visual FoxPro によってエラーが生成されます。  
  
 一意の *eExpression3*タグ *TagName3*  
 候補インデックスを作成します。 *eExpression3* は、テーブル内のフィールドまたはフィールドの組み合わせを指定します。 ただし、主キーオプションのいずれかを使用してプライマリインデックスを作成した場合は、プライマリインデックスに対して指定されたフィールドを含めることはできません。 タグ *TagName3* 作成される候補のインデックスタグのタグ名を指定します。 インデックスタグ名には、最大10文字まで含めることができます。  
  
 テーブルには複数の候補インデックスを含めることができます。  
  
 外部キー *eExpression4*TAG *TagName4*[nodup]  
 外部 (非プライマリ) インデックスを作成し、親テーブルとのリレーションシップを確立します。 *eExpression4* は、外部インデックスキーの式を指定し、 *TagName4* は、作成される外部インデックスキータグの名前を指定します。 インデックスタグ名には、最大10文字まで含めることができます。 候補の外部インデックスを作成するには、NODUP を含めます。  
  
 テーブルに対して複数の外部インデックスを作成できますが、外部インデックス式ではテーブル内の別のフィールドを指定する必要があります。  
  
 *TableName3*の参照 [TAG *TagName5*]  
 永続的なリレーションシップを確立する親テーブルを指定します。 親テーブルのインデックスタグに基づいてリレーションシップを確立するには、タグ *TagName5* を含めます。 インデックスタグ名には、最大10文字まで含めることができます。 既定では、TAG *TagName5 を* 省略すると、親テーブルのプライマリインデックスキーを使用してリレーションシップが確立されます。  
  
 *EExpression2*の確認 [ERROR *cMessageText2*]  
 テーブル検証ルールを指定します。 エラー *cMessageText2* は、テーブル検証ルールが実行されたときに Visual FoxPro によって表示されるエラーメッセージを指定します。 このメッセージは、[参照] ウィンドウまたは [編集] ウィンドウ内でデータが変更された場合にのみ表示されます。  
  
 配列*Arrayname*から  
 テーブル内の各フィールドの名前、型、有効桁数、および小数点以下桁数を内容とする既存の配列の名前を指定します。 配列の内容は、 **Afields**() 関数を使用して定義できます。  
  
## <a name="remarks"></a>解説  
 新しいテーブルは、使用可能な最も低い作業領域で開かれ、そのエイリアスによってアクセスできます。 新しいテーブルは、SET EXCLUSIVE の現在の設定に関係なく、排他的に開かれます。  
  
 データベースが開いていて、FREE 句が含まれていない場合は、新しいテーブルがデータベースに追加されます。 データベース内のテーブルと同じ名前の新しいテーブルを作成することはできません。  
  
 データベースが開いている場合、CREATE TABLE SQL では、データベースを排他的に使用する必要があります。 排他的に使用するためにデータベースを開くには、OPEN DATABASE に EXCLUSIVE を含めます。  
  
 新しいテーブルを作成するときにデータベースが開かれていない場合は、名前、CHECK、DEFAULT、FOREIGN KEY、PRIMARY KEY、または REFERENCES の各句を指定すると、エラーが生成されます。  
  
> [!NOTE]  
>  CREATE TABLE 構文では、特定の CREATE TABLE オプションを区切るためにコンマが使用されます。 また、null、NOT NULL、CHECK、DEFAULT、PRIMARY KEY、および UNIQUE 句は、列定義を含むかっこ内に配置する必要があります。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションが ODBC SQL ステートメント CREATE TABLE をデータソースに送信すると、Visual FoxPro ODBC ドライバーは、次の表に示す構文を使用して、コマンドを Visual FoxProCREATE TABLE コマンドに変換します。  
  
|ODBC 構文|Visual FoxPro の構文|  
|-----------------|--------------------------|  
|CREATE TABLE *のベーステーブル名*<br /><br /> (*列識別子データ型*<br /><br /> [NULL 以外]<br /><br /> [,*列識別子データ型*<br /><br /> [NULL 以外]...)|CREATE TABLE *TableName1* [名前 *longtablename*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*Nfieldwidth* [, *nprecision*])]<br /><br /> [NULL 以外])|  
  
 ドライバーを使用してテーブルを作成する場合、ドライバーは、作成後すぐにテーブルを閉じて、他のユーザーがテーブルにアクセスできるようにします。 これは Visual FoxPro とは異なり、テーブルは作成時に排他的に開かれたままになります。 ただし、CREATE TABLE ステートメントを含むデータソースのストアドプロシージャを実行すると、そのテーブルは開いたままになります。  
  
 データソースがデータベース (dbc ファイル) の場合、Visual FoxPro ODBC ドライバーは、*ベーステーブル名*と同じ名前の*longtablename*という名前のテーブルを作成します。  
  
### <a name="using-data-definition-language-ddl"></a>データ定義言語 (DDL) の使用  
 次の場所に DDL を含めることはできません。  
  
-   トランザクションを必要とするバッチ SQL ステートメントの場合  
  
-   手動コミットモードでは、トランザクションを必要とするステートメントの後、アプリケーションが最初に **Sqltransact**を呼び出す場合を除きます。  
  
 たとえば、一時テーブルを作成する場合は、トランザクションを必要とするステートメントを開始する前に、テーブルを作成する必要があります。 トランザクションを必要とするバッチ SQL ステートメントに CREATE TABLE ステートメントを含めると、ドライバーはエラーメッセージを返します。  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE-SQL コマンド](../../odbc/microsoft/alter-table-sql-command.md)   
 [サポートされているデータ型 (Visual FoxPro ODBC ドライバー)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT-SQL コマンド](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL コマンド](../../odbc/microsoft/select-sql-command.md)
