---
description: SQL ステートメントで使用される要素
title: SQL ステートメントで使用される要素 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c24f5dd55530e38ea47ed9a2b846d549bb26d56
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456575"
---
# <a name="elements-used-in-sql-statements"></a>SQL ステートメントで使用される要素
次の要素は、前に示した SQL ステートメントで使用されています。  
  
## <a name="element"></a>要素  
 *ベーステーブル識別子* :: = *ユーザー定義-名前*  
  
 *base-table-name* :: = *base-テーブル識別子*  
  
 *ブール値* :: = [NOT] *ブール値のプライマリ*  
  
 *ブール値-primary* :: = 比較 *-述語* &#124; ( *検索条件* )  
  
 *ブール値-* : = *ブール値* [AND *boolean-term*]  
  
 *文字文字列-リテラル* :: = ' ' {*character*}... ' ' (*文字* は、ドライバー/データソースの文字セット内の任意の文字です。 1つのリテラル引用符文字 (' ') を文字文字列リテラルに含めるには、2つのリテラル引用符文字 (' ' ' ') を使用します。  
  
 *列識別子* :: = *ユーザー定義-名前*  
  
 *列名* :: = [*テーブル名*]*列識別子*  
  
 *比較演算子* :: = < &#124; > &#124; \<= &#124; > = &#124; = &#124; <>  
  
 *比較-述語* :: = *式* の比較-演算子式  
  
 *データ型* :: = *文字文字列型* (*文字文字列型* ) は任意のデータ型で、SQLGetTypeInfo によって返される結果セットの "DATA_TYPE" "列が SQL_CHAR または SQL_VARCHAR になります。  
  
 *digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *動的パラメーター* :: =?  
  
 *expression* :: = term &#124; 式 {+&#124;-} term  
  
 *factor* :: = [ *+*&#124;*-* ]*プライマリ*  
  
 *挿入-値* :: =  
  
 *動的パラメーター*  
  
 &#124; *リテラル*  
  
 &#124; NULL  
  
 &#124; ユーザー  
  
 *文字* :: = 小文字の大文字 &#124; 大文字/ *小文字*  
  
 *literal* :: = *文字文字列-リテラル*  
  
 *小文字* :: = a &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *order by 句* :: = order by *sort-specification* [, *sort-specification*]...  
  
 *primary* :: = *列名*  
  
 &#124; *動的パラメーター*  
  
 &#124; *リテラル*  
  
 &#124; ( *式* )  
  
 *検索条件* :: = *ブール値* [OR *検索条件*]  
  
 *select-list* :: = \* &#124; *選択-サブリスト* [, *選択-サブリスト*]... (*選択リストに* パラメーターを含めることはできません)。  
  
 *select-サブリスト* :: = *式*  
  
 *並べ替え-指定* :: = {*符号なし-整数 &#124; 列名*} [*ASC &#124; DESC*]  
  
 *テーブル識別子* :: = *ユーザー定義-名前*  
  
 *テーブル名* :: = *テーブル識別子*  
  
 *テーブル参照* :: = *テーブル名*  
  
 *テーブル参照-リスト* :: = *テーブル参照* [,*テーブル参照*]...  
  
 *term* :: = *factor* &#124; *term* { \*&#124;*/* } *係数*  
  
 *符号なし整数* :: = {*digit*}  
  
 *大文字と小文字* :: = *A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; I &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; P &#124; &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *ユーザー定義-名前* :: = *文字*[*数字* &#124; *文字* &#124; *_*]...
