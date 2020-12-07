---
description: ALTER TABLE - SQL コマンド
title: ALTER TABLE-SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c72d03abff792ff103bf009cd12b718c74bd497d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483705"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL コマンド
プログラムによってテーブルの構造を変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>引数  
 *TableName1*  
 構造が変更されたテーブルの名前を指定します。  
  
 ADD [COLUMN] *FieldName1*  
 追加するフィールドの名前を指定します。  
  
 ALTER [COLUMN] *FieldName1*  
 変更する既存のフィールドの名前を指定します。  
  
 *FieldType* [( *nfieldwidth* [, *nprecision*]])  
 新規または変更されたフィールドのフィールドの種類、フィールドの幅、およびフィールドの有効桁数 (小数点以下桁数) を指定します。  
  
 *FieldType* は、フィールドの [データ型](../../odbc/microsoft/visual-foxpro-field-data-types.md)を示す単一の文字です。 一部のフィールドデータ型では、 *Nfieldwidth* または *nprecision* またはその両方を指定する必要があります。  
  
 *Nfieldwidth* と *Nprecision* は、D、G、I、L、M、P、T、および Y 型では無視されます。 既定では、n*精度が B* 、F、または N 型に含まれていない場合、 *nprecision*はゼロ (小数点以下の桁数なし) になります。  
  
 NULL &#124; NOT NULL  
 フィールドの null 値を許可または禁止します。  
  
 Null と NOT NULL を省略すると、SET NULL の現在の設定によって、フィールドで null 値が許可されるかどうかが決まります。 ただし、null および NOT NULL を省略し、PRIMARY KEY または UNIQUE 句を含めると、SET NULL の現在の設定は無視され、既定では、このフィールドは NULL になりません。  
  
 *LExpression1*の確認  
 フィールドの検証規則を指定します。 *lExpression1* は論理式に評価される必要があり、ユーザー定義関数またはストアドプロシージャを指定できます。 空白のレコードが追加されるたびに、検証規則がチェックされます。 追加されたレコードで空のフィールド値が検証規則によって許可されていない場合、エラーが生成されます。  
  
 エラー *cMessageText1*  
 フィールド検証規則によってエラーが生成された場合に表示されるエラーメッセージを指定します。  
  
 既定の *eExpression1*  
 フィールドの既定値を指定します。 *EExpression1*のデータ型は、フィールドのデータ型と同じである必要があります。  
  
 PRIMARY KEY  
 プライマリインデックスタグを作成します。 インデックスタグには、フィールドと同じ名前が付けられています。  
  
 UNIQUE  
 フィールドと同じ名前の候補インデックスタグを作成します。  
  
> [!NOTE]  
>  (ALTER TABLE または CREATE TABLE の ANSI 互換性のために、UNIQUE オプションを含めることによって作成された) 候補インデックスは、INDEX コマンドで UNIQUE オプションを使用して作成されたインデックスとは異なります。 Index コマンドで UNIQUE を使用して作成されたインデックスでは、重複するインデックスキーが許可されます。候補インデックスでは、重複するインデックスキーは許可されません。  
  
 プライマリインデックスまたは候補インデックスに使用されるフィールドでは、Null 値と重複レコードは許可されません。  
  
 [列の追加] を使用して新しいフィールドを作成する場合、null 値をサポートするフィールドのプライマリインデックスまたは候補インデックスを作成しても、Visual FoxPro ではエラーは生成されません。 ただし、プライマリインデックスまたは候補インデックスに使用するフィールドに null 値または重複値を入力しようとすると、エラーが発生します。  
  
 既存のフィールドを変更し、主または候補のインデックス式がテーブル内のフィールドで構成されている場合、Visual FoxPro はフィールドをチェックして、null 値が含まれているか、レコードが重複していないかを確認します。 そうしないと、Visual FoxPro によってエラーが生成され、テーブルは変更されません。  
  
 *TableName2*タグ*TagName1*の参照  
 永続的なリレーションシップを確立する親テーブルを指定します。 タグ *TagName1* 、リレーションシップの基になる親テーブルのインデックスタグを指定します。 インデックスタグ名には、最大10文字まで含めることができます。  
  
 NOCPTRANS  
 文字フィールドとメモフィールドの別のコードページに変換できないようにします。 テーブルを別のコードページに変換した場合、NOCPTRANS が指定されているフィールドは翻訳されません。 NOCPTRANS は、文字フィールドとメモフィールドに対してのみ指定できます。  
  
 次の例では、2つの文字フィールドと2つのメモフィールドを含む、mytable という名前のテーブルを作成します。 2番目の文字フィールド、char2、および2番目のメモフィールド memo2 には、変換を防止するための NOCPTRANS が含まれています。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 変更する既存のフィールドの名前を指定します。  
  
 既定の*eExpression2*の設定  
 既存のフィールドの新しい既定値を指定します。 *EExpression2*のデータ型は、フィールドのデータ型と同じである必要があります。  
  
 SET CHECK *lExpression2*  
 既存のフィールドの新しい検証規則を指定します。 *lExpression2* は論理式に評価される必要があり、ユーザー定義関数またはストアドプロシージャである可能性があります。  
  
 エラー *cMessageText2*  
 フィールド検証規則によってエラーが生成された場合に表示されるエラーメッセージを指定します。 このメッセージは、[参照] ウィンドウまたは [編集] ウィンドウ内でデータが変更された場合にのみ表示されます。  
  
 DROP DEFAULT  
 既存のフィールドの既定値を削除します。  
  
 削除の確認  
 既存のフィールドの検証規則を削除します。  
  
 DROP [列] *FieldName3*  
 テーブルから削除するフィールドを指定します。 テーブルからフィールドを削除すると、フィールドの既定値の設定とフィールドの検証規則も削除されます。  
  
 インデックスキーまたはトリガー式がフィールドを参照している場合、フィールドが削除されると、式は無効になります。 この場合、フィールドを削除してもエラーは生成されませんが、無効なインデックスキーまたはトリガー式によって実行時にエラーが発生します。  
  
 SET CHECK *lExpression3*  
 テーブル検証ルールを指定します。 *lExpression3* は論理式に評価される必要があり、ユーザー定義関数またはストアドプロシージャである可能性があります。  
  
 エラー *cMessageText3*  
 テーブル検証ルールがエラーを生成したときに表示されるエラーメッセージを指定します。 このメッセージは、[参照] ウィンドウまたは [編集] ウィンドウ内でデータが変更された場合にのみ表示されます。  
  
 削除の確認  
 テーブルの検証規則を削除します。  
  
 主キー *eExpression3*タグ*TagName2*の追加  
 テーブルにプライマリインデックスを追加します。 *eExpression3* は、主インデックスキーの式を指定し、 *TagName2* はプライマリインデックスタグの名前を指定します。 インデックスタグ名には、最大10文字まで含めることができます。 TAG *TagName2* が省略され、 *eExpression3* が1つのフィールドである場合、プライマリインデックスタグは *eExpression3*で指定されたフィールドと同じ名前になります。  
  
 主キーの削除  
 プライマリインデックスとそのインデックスタグを削除します。 テーブルには主キーを1つしか含めることができないため、主キーの名前を指定する必要はありません。 プライマリインデックスを削除すると、主キーに基づくすべての永続的な関係も削除されます。  
  
 UNIQUE *eExpression4*の追加 [TAG *TagName3*]  
 候補インデックスをテーブルに追加します。 *eExpression4* は候補インデックスキー式を指定し、 *TagName3* は候補のインデックスタグの名前を指定します。 インデックスタグ名には、最大10文字まで含めることができます。 TAG *TagName3* を省略し、 *eExpression4* が1つのフィールドである場合、候補インデックスタグの名前は *eExpression4*で指定されたフィールドと同じになります。  
  
 一意のタグの削除 *TagName4*  
 候補インデックスとそのインデックスタグを削除します。 テーブルには複数の候補キーを含めることができるので、候補のインデックスタグの名前を指定する必要があります。  
  
 外部キー [ *eExpression5*] タグ*TagName4*の追加  
 外部 (非プライマリ) インデックスをテーブルに追加します。 *eExpression5* は、外部インデックスキーの式を指定し、 *TagName4* は外部インデックスタグの名前を指定します。 インデックスタグ名には、最大10文字まで含めることができます。  
  
 *TableName2*の参照 [TAG *TagName5*]  
 永続的なリレーションシップを確立する親テーブルを指定します。 親テーブルの既存のインデックスタグに基づいてリレーションシップを確立するには、タグ *TagName5* を含めます。 インデックスタグ名には、最大10文字まで含めることができます。 タグ *TagName5*を省略した場合、リレーションシップは親テーブルのプライマリインデックスタグを使用して確立されます。  
  
 外部キータグ *TagName6*の削除 [保存]  
 インデックスタグが *TagName6*である外部キーを削除します。 [保存] を省略した場合、インデックスタグは構造インデックスから削除されます。 構造インデックスからインデックスタグが削除されないようにするには、[保存する。  
  
 列の名前を*FieldName4*から*FieldName5*に変更します。  
 テーブル内のフィールドの名前を変更できます。 *FieldName4* 名前を変更するフィールドの名前を指定します。 *FieldName5* フィールドの新しい名前を指定します。  
  
> [!CAUTION]  
>  インデックス式、フィールドとテーブルの検証規則、コマンド、および関数が元のフィールド名を参照する可能性があるため、テーブルフィールドの名前を変更するときは注意してください。  
  
 NOVALIDATE  
 Visual FoxPro で、テーブルの構造に変更を加えることを許可することを指定します。これらの変更は、テーブル内のデータの整合性に違反している可能性があります。 既定では、ALTER TABLE によってテーブル内のデータの整合性に違反する変更が行われないようにします。 この既定の動作をオーバーライドするには、NOVALIDATE を含めます。  
  
## <a name="remarks"></a>解説  
 ALTER TABLE を使用して、データベースに追加されていないテーブルの構造を変更できます。 ただし、free テーブルを変更するときに、既定、外部キー、主キー、参照、または SET 句を含めると、エラーが生成されます。  
  
 ALTER TABLE では、新しいテーブルヘッダーを作成し、テーブルヘッダーにレコードを追加することによって、テーブルを再構築できます。 たとえば、フィールドの型または幅を変更すると、テーブルが再構築される可能性があります。  
  
 テーブルを再構築すると、型または幅が変更されたフィールドに対してフィールド検証規則が実行されます。 テーブル内のフィールドの型または幅を変更すると、テーブルルールが実行されます。  
  
 レコードがあるテーブルに対してフィールドまたはテーブルの検証ルールを変更すると、Visual FoxPro は、既存のデータに対して新しいフィールドまたはテーブルの検証ルールをテストし、フィールドまたはテーブルの検証ルールまたはトリガー違反の最初の発生時に警告を発行します。  
  
 変更するテーブルがデータベース内にある場合、ALTER TABLE-SQL では、データベースを排他的に使用する必要があります。 排他的に使用するためにデータベースを開くには、OPEN DATABASE に EXCLUSIVE を含めます。  
  
## <a name="see-also"></a>関連項目  
 [CREATE TABLE-SQL コマンド](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX コマンド](../../odbc/microsoft/index-command.md)
