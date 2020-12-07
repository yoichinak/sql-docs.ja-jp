---
description: Shape の正式文法
title: 仮形の文法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: rothja
ms.author: jroth
ms.openlocfilehash: be65ff094518defcbf27ba2aa2ffa69835ee8ca3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991273"
---
# <a name="formal-shape-grammar"></a>Shape の正式文法
これは、任意のシェイプコマンドを作成するための正式な文法です。  
  
-   必須の文法用語は、山かっこ ("<>") で区切られたテキスト文字列です。  
  
-   省略可能な語句は、角かっこ ("[]") で区切られます。  
  
-   代替手段は、"&#124;" によって示されます。  
  
-   代替の繰り返しは、省略記号 ("...") で示されます。  
  
-   *Alpha* は、アルファベットの文字列を示します。  
  
-   *数字* は、数字の文字列を示します。  
  
-   *Unicode* 数字は、unicode の数字の文字列を示します。  
  
 それ以外のすべての用語はリテラルです。  
  
|期間|定義|  
|----------|----------------|  
|\<shape-command>|図形 [ \<table-exp> []]] \<alias> [ \<shape-action> ]|  
|\<table-exp>|{ \<provider-command-text> } &#124;<br /><br /> ( \<shape-command> ) &#124;<br /><br /> テーブル \<quoted-name> &#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|&#124; の追加 \<aliased-field-list><br /><br /> COMPUTE \<aliased-field-list> [BY \<field-list> ]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias> ]|  
|\<field-exp>|( \<relation-exp> ) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias> ]<br /><br /> 関する \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> 宛先 \<child-ref>|  
|\<child-ref>|\<field-name> &#124;<br /><br /> 引き \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM ( \<qualified-field-name> ) &#124;<br /><br /> AVG ( \<qualified-field-name> ) &#124;<br /><br /> MIN ( \<qualified-field-name> ) &#124;<br /><br /> MAX ( \<qualified-field-name> ) &#124;<br /><br /> カウント ( \<qualified-alias> &#124; \<qualified-name> ) &#124;<br /><br /> STDEV ( \<qualified-field-name> ) &#124;<br /><br /> ANY ( \<qualified-field-name> )|  
|\<calculated-exp>|CALC ( \<expression> )|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias> ]|  
|\<quoted-name>|" \<string> " &#124;<br /><br /> ' \<string> ' &#124;<br /><br /> [ \<string> ] &#124;<br /><br /> \<name>|  
|\<qualified-name>|エイリアス [. alias...]|  
|\<name>|alpha [α &#124; digit &#124; _ &#124; # &#124;: &#124;...]|  
|\<number>|数字 [digit...]|  
|\<new-exp>|NEW \<field-type> [( \<number> [, \<number> ])]|  
|\<field-type>|OLE DB または ADO データ型。|  
|\<string>|unicode-char [unicode-char...]|  
|\<expression>|同じ行の他の非計算列であるオペランドを持つ Visual Basic for Applications 式。|  
  
## <a name="see-also"></a>参照  
 [階層レコードセット内の行へのアクセス](./accessing-rows-in-a-hierarchical-recordset.md)   
 [データシェイプの概要](./data-shaping-overview.md)   
 [データシェイプに必要なプロバイダー](./required-providers-for-data-shaping.md)   
 [Shape APPEND 句](./shape-append-clause.md)   
 [一般的なシェイプコマンド](./shape-commands-in-general.md)   
 [Shape COMPUTE 句](./shape-compute-clause.md)   
 [Visual Basic for Applications の関数](./visual-basic-for-applications-functions.md)