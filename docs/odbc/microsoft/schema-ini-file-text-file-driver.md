---
description: Schema.ini ファイル (テキスト ファイル ドライバー)
title: Schema.ini ファイル (テキストファイルドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b4bbebfa6eb184bf81cba4a9faf5e3200f428de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500225"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini ファイル (テキスト ファイル ドライバー)
テキストドライバーが使用されている場合、テキストファイルの形式はスキーマ情報ファイルを使用して決定されます。 スキーマ情報ファイルは常に Schema.ini という名前であり、常にテキストデータソースと同じディレクトリに保持されます。 スキーマ情報ファイルでは、ファイルの一般的な形式、列名とデータ型の情報、およびその他のいくつかのデータ特性に関する情報が IISAM に提供されます。 固定長のデータにアクセスするには、常に Schema.ini ファイルが必要です。 テキストテーブルに日時、通貨、または10進数のデータが含まれている場合、またはテーブル内のデータの処理をより細かく制御する必要がある場合は、Schema.ini ファイルを使用する必要があります。  
  
> [!NOTE]  
>  テキスト ISAM は、Schema.ini からではなく、レジストリから初期値を取得します。 すべての新しいテキストデータテーブルには、同じ既定のファイル形式が適用されます。 CREATE TABLE ステートメントによって作成されたすべてのファイルは、同じ既定の形式の値を継承します。これらの値は、[テーブル] ボックスで選択した [**テキスト形式の定義**] ダイアログボックスで [ファイル形式] の値を選択することによって設定され \<default> ます**Tables** 。 レジストリの値が Schema.ini の値と異なる場合は、レジストリの値が Schema.ini の値によって上書きされます。  
  
## <a name="understanding-schemaini-files"></a>Schema.ini ファイルについて  
 Schema.ini ファイルは、テキストファイル内のレコードに関するスキーマ情報を提供します。 各 Schema.ini エントリは、次の5つの表のいずれかの特性を指定します。  
  
-   テキストファイル名  
  
-   ファイル形式  
  
-   フィールド名、幅、および型  
  
-   文字セット  
  
-   特殊なデータ型変換  
  
 以下のセクションでは、これらの特性について説明します。  
  
## <a name="specifying-the-file-name"></a>ファイル名の指定  
 Schema.ini の最初のエントリは常に、角かっこで囲まれたテキストソースファイルの名前です。 次の例は、Sample.txt ファイルのエントリを示しています。  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>ファイル形式の指定  
 Schema.ini の **format** オプションでは、テキストファイルの形式を指定します。 Text IISAM は、ほとんどの文字区切りファイルから自動的に形式を読み取ることができます。 ファイルでは、二重引用符 (") 以外の任意の1文字を区切り記号として使用できます。 Schema.ini の [ **形式** ] 設定では、Windows レジストリの設定 (ファイル別) が上書きされます。 次の表に、 **Format** オプションの有効な値を示します。  
  
|書式指定子|テーブル形式|Schema.ini Format ステートメント|  
|----------------------|------------------|---------------------------------|  
|**タブ区切り**|ファイル内のフィールドはタブで区切られます。|Format = TabDelimited れた|  
|**CSV 区切り**|ファイル内のフィールドはコンマで区切られます (コンマ区切り値)。|Format = CSVDelimited|  
|**区切られたカスタム**|ファイル内のフィールドは、ダイアログボックスに入力するために選択した任意の文字で区切られます。 空白を含め、二重引用符 (") 以外のすべてが許可されます。|Format = 区切られた (*カスタム文字*)<br /><br /> - または -<br /><br /> 区切り記号が指定されていない場合:<br /><br /> Format = 区切られた ()|  
|**固定長**|ファイルのフィールドの長さは固定されています。|Format = FixedLength|  
  
## <a name="specifying-the-fields"></a>フィールドの指定  
 次の2つの方法で、文字区切りのテキストファイルにフィールド名を指定できます。  
  
-   テーブルの最初の行にフィールド名を含め、 **Colnameheader** を True に設定し **ます。**  
  
-   各列を数値で指定し、列名とデータ型を指定します。  
  
 各列を数値で指定し、固定長ファイルの列名、データ型、および幅を指定する必要があります。  
  
> [!NOTE]  
>  Schema.ini の **Colnameheader** 設定は、Windows レジストリの **FirstRowHasNames** 設定をファイル別に上書きします。  
  
 フィールドのデータ型を特定することもできます。 **MaxScanRows**オプションを使用して、列の型を決定するときにスキャンする行数を指定します。 **MaxScanRows**を0に設定すると、ファイル全体がスキャンされます。 Schema.ini の **MaxScanRows** 設定は、Windows レジストリの設定 (ファイル別) を上書きします。  
  
 次のエントリは、Microsoft Jet がテーブルの最初の行のデータを使用してフィールド名を決定し、ファイル全体を調べて使用されるデータ型を確認する必要があることを示しています。  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 次のエントリでは、列番号 (**Col**_n_) オプションを使用してテーブル内のフィールドを指定します。このオプションは、文字区切りファイルの場合は省略可能であり、固定長のファイルでは必須です。 この例では、次の2つのフィールドの Schema.ini エントリ、10文字の顧客番号テキストフィールド、および30文字のテキストフィールドが表示されます。  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 **Col**_n_の構文は次のとおりです。  
  
```  
  
n=ColumnName type [Width] [#]  
```  
  
## <a name="remarks"></a>解説  
 次の表では、 **Col**_n_ エントリの各部分について説明します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*[ColumnName]*|列のテキスト名。 列名にスペースが埋め込まれている場合は、二重引用符で囲む必要があります。|  
|*type*|データ型は次のとおりです。<br /><br /> **Microsoft Jet データ型**<br /><br /> ビット<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> Currency<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Text<br /><br /> メモ<br /><br /> **ODBC データ型** Char (テキストと同じ)<br /><br /> Float (Double と同じ)<br /><br /> 整数 (Short と同じ)<br /><br /> LongChar (Memo と同じ)<br /><br /> 日付の *日付形式*|  
|**Width**|リテラル文字列値 `Width` 。 次の数値が列の幅を指定することを示します (文字区切りファイルの場合は省略可能、固定長ファイルの場合は必須)。|  
|*#*|列の幅を指定する整数値 ( **幅** が指定されている場合は必須)。|  
  
## <a name="selecting-a-character-set"></a>文字セットの選択  
 ANSI と OEM の2つの文字セットから選択できます。 Schema.ini の **CharacterSet** 設定は、Windows レジストリの設定 (ファイル別) を上書きします。 次の例は、文字セットを ANSI に設定する Schema.ini エントリを示しています。  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>データ型の形式と変換の指定  
 Schema.ini ファイルには、データの変換方法や表示方法を指定するために使用できるオプションがいくつか含まれています。 次の表に、これらの各オプションの一覧を示します。  
  
|オプション|説明|  
|------------|-----------------|  
|**DateTimeFormat**|日付と時刻を示す書式文字列を設定できます。 インポート/エクスポートのすべての日付/時刻フィールドが同じ形式で処理される場合は、このエントリを指定する必要があります。 すべての Microsoft Jet 形式 (午前を除く) 午後の時刻の がサポートされます。 書式設定文字列がない場合は、Windows の [コントロールパネル] の [短い日付の画像と時刻] オプションが使用されます。|  
|**DecimalSymbol**|数値の小数部から整数を区切るために使用される任意の1文字に設定できます。|  
|**数字**|数値の小数部の小数点以下の桁数を示します。|  
|**数値のリードのゼロ**|1未満の10進値に先行ゼロを含めるかどうかを指定します。この値には、False (先行ゼロなし) または True を指定できます。|  
|**CurrencySymbol**|テキストファイル内の通貨の値に使用できる通貨記号を示します。 例としては、ドル記号 ($) と Dm などがあります。|  
|**CurrencyPosFormat**|次のいずれかの値に設定できます。<br /><br /> -区切りなしの通貨記号プレフィックス ($1)<br />-区切りなしの通貨記号のサフィックス ($1)<br />-1 文字の区切り記号を使用した通貨記号のプレフィックス ($1)<br />-1 文字の区切り記号を含む通貨記号のサフィックス ($1)|  
|**CurrencyDigits**|通貨金額の小数部に使用する桁数を指定します。|  
|**CurrencyNegFormat**|次の値のいずれかです。<br /><br /> -($1)<br />--$1<br />-$-1<br />-$1-<br />-($1)<br />--$1<br />-1-$<br />-$1-<br />--$1<br />--$1<br />-$1-<br />-$1-<br />-$-1<br />-1-$<br />-($1)<br />-($1)<br /><br /> この例ではドル記号を示していますが、実際のプログラムでは、適切な **CurrencySymbol** 値に置き換える必要があります。|  
|**CurrencyThousandSymbol**|テキストファイル内の通貨値を千単位で区切るために使用できる1文字の記号を示します。|  
|**CurrencyDecimalSymbol**|通貨値の小数部分から全体を区切るために使用される任意の1文字に設定できます。|  
  
> [!NOTE]  
>  エントリを省略した場合は、Windows のコントロールパネルの既定値が使用されます。
