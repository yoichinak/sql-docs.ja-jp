---
description: テキスト ファイルの形式 (テキスト ファイル ドライバー)
title: テキストファイル形式 (テキストファイルドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb402f0f186529da33974b77ffeecdd7ed788d53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449094"
---
# <a name="text-file-format-text-file-driver"></a>テキスト ファイルの形式 (テキスト ファイル ドライバー)
ODBC テキストドライバーでは、区切り文字と固定幅のテキストファイルの両方がサポートされています。 テキストファイルは、省略可能なヘッダー行と0個以上のテキスト行で構成されます。  
  
 ヘッダー行ではテキストファイル内の他の行と同じ形式が使用されますが、ODBC テキストドライバーはヘッダー行エントリをデータではなく列名として解釈します。  
  
 区切られたテキスト行には、コンマ、タブ、またはカスタムの区切り記号で区切られた1つ以上のデータ値が含まれます。 ファイル全体で同じ区切り記号を使用する必要があります。 Null データ値は、行の間にデータがない2つの区切り記号によって示されます。 区切られたテキスト行の文字列は、二重引用符 ("") で囲むことができます。 区切られた値の前または後に空白を使用することはできません。  
  
 固定幅のテキスト行の各データエントリの幅は、スキーマで指定されます。 Null データ値は空白で示されます。  
  
 テーブルは、最大255のフィールドに制限されています。 フィールド名は64文字に制限されており、フィールドの幅は32766文字に制限されています。 レコードのサイズは65000バイトに制限されています。  
  
 1人のユーザーに対してのみ、テキストファイルを開くことができます。 複数のユーザーはサポートされていません。  
  
 プログラマ向けに記述された次の文法は、ODBC テキストドライバーで読み取ることができるテキストファイルの形式を定義しています。  
  
|形式|[表記]|  
|------------|--------------------|  
|斜体以外|表示されるように入力する必要がある文字|  
|*付き*|文法の別の場所で定義された引数|  
|角かっこ ([])|省略可能な項目|  
|中かっこ ( {} )|相互に排他的な選択肢の一覧|  
|縦棒 (&#124;)|相互に排他的な選択肢を分離する|  
|省略記号 (...)|1回以上繰り返すことができる項目|  
  
 テキストファイルの形式は次のとおりです。  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  固定幅テキストファイルの各列の幅は、Schema.ini ファイルで指定されます。  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  カスタム区切りのテキストファイルの区切り記号は、Schema.ini ファイルに指定されています。  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  区切られたファイルの場合、NULL は2つの区切り記号の間にデータがないことで表されます。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  固定幅ファイルの場合、NULL はスペースで表されます。
