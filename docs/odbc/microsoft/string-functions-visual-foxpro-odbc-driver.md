---
description: 文字列関数 (Visual FoxPro ODBC ドライバー)
title: 文字列関数 (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ab2ecefb604183b0387a561f72494028c62d15f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471544"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>文字列関数 (Visual FoxPro ODBC ドライバー)
次の表に、Visual FoxPro ODBC ドライバーでサポートされている ODBC 文字列操作関数の一覧を示します。同じ関数の Visual FoxPro 文法が ODBC 構文と異なる場合は、Visual FoxPro と同等のものが表示されます。  
  
|ODBC 文法|Visual FoxPro の文法|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(コード)*|CHR *(string_exp)*|  
|CONCAT *(string_exp1、string_exp2)*|*string_exp1 + string_exp2*|  
|相違点 *(string_exp1、string_exp2)*||  
|INSERT *(string_exp1、start、length、string_exp2)*|*(String_exp1、開始、長さ、string_exp2)*|  
|LCASE *(string_exp)*|LOWER *(string_exp)*|  
|LEFT *(string_exp, count)*||  
|長さ *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|REPEAT *(string_exp, count)*|REPLICATE *(string_exp, count)*|  
|REPLACE *(string_exp1、string_exp2、string_exp3)*|STRTRAN *(string_exp1、string_exp2、string_exp3)*|  
|RIGHT *(string_exp、count)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|領域 *(カウント)*||  
|SUBSTRING *(string_exp、start、length)*|SUBSTR *(string_exp、start、length)*|  
|UCASE *(string_exp)*|UPPER *(string_exp)*|
