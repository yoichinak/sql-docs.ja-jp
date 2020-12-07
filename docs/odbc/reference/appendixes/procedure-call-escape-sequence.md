---
description: プロシージャ呼び出しのエスケープ シーケンス
title: プロシージャ呼び出しのエスケープシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba88f3d78edeaa1ce4f4884977656cd8a4a16062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483225"
---
# <a name="procedure-call-escape-sequence"></a>プロシージャ呼び出しのエスケープ シーケンス
ODBC では、プロシージャ呼び出しにエスケープシーケンスを使用します。 このエスケープシーケンスの構文は次のとおりです。  
  
 **{**[? =]**呼び出し***プロシージャ名*[**(**[*parameter*] [, [*parameter*]]...**)**]**}**  
  
 BNF 表記では、構文は次のようになります。  
  
 *ODBC-プロシージャエスケープ* :: =  
  
 &#124; *odbc-esc-イニシエーター* [? =] プロシージャを呼び出す *odbc-esc-ターミネータ*  
  
 *プロシージャ* :: = *プロシージャ名* &#124; *プロシージャ名* (*プロシージャパラメーターリスト*)  
  
 *プロシージャ識別子* :: = *ユーザー定義-名前*  
  
 *プロシージャ名* :: = *プロシージャ識別子*  
  
 &#124; *所有者名*。*プロシージャ-識別子*  
  
 &#124; *catalog-name catalog-separator* *プロシージャ-identifier*  
  
 &#124; *catalog-name catalog-separator* [*owner-name*]」と入力します。*プロシージャ-識別子*  
  
 (3 番目の構文は、データソースで所有者がサポートされていない場合にのみ有効です)。  
  
 *所有者名* :: = *ユーザー定義-名前*  
  
 *カタログ名* :: = *ユーザー定義-名前*  
  
 *catalog-separator* :: = {*implementation defined*}  
  
 (カタログ区切り記号は、SQL_CATALOG_NAME_SEPARATOR information オプションと共に **SQLGetInfo** 経由で返されます)。  
  
 *プロシージャパラメーター-list* :: = *procedure-parameter*  
  
 &#124; *プロシージャパラメーター*、 *プロシージャパラメーターリスト*  
  
 *プロシージャパラメーター* :: = *動的パラメーター* &#124; *リテラル* &#124; *空文字列*  
  
 *空の文字列* :: =  
  
 *ODBC-esc-イニシエーター* :: = {  
  
 *ODBC-esc-ターミネータ* :: =}  
  
 (プロシージャパラメーターが空の文字列の場合、プロシージャはそのパラメーターの既定値を使用します)。  
  
 データソースがプロシージャをサポートしているかどうか、およびドライバーが ODBC プロシージャ呼び出し構文をサポートしているかどうかを判断するために、アプリケーションは SQL_PROCEDURES 情報型を使用して **SQLGetInfo** を呼び出すことができます。
