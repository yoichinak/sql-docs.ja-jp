---
description: 列名の制限
title: 列名の制限 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 82cac260fc81ce5a2cfbbe3e4c3c0bdab5a47049
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483695"
---
# <a name="column-name-limitations"></a>列名の制限
列名には、任意の有効な文字 (たとえば、スペース) を含めることができます。 列名に文字、数字、およびアンダースコア以外の文字が含まれている場合は、名前を引用符 (') で囲むことによって区切る必要があります。  
  
 Microsoft Access または Microsoft Excel driver が使用されている場合、列名は64文字に制限され、長い名前ではエラーが発生します。 Paradox ドライバーが使用されている場合、列の最大名は25文字です。 テキストドライバーが使用されている場合、列の最大名は64文字で、長い名前は切り捨てられます。  
  
 DBASE ドライバーを使用すると、ASCII 値が127より大きい文字はアンダースコアに変換されます。  
  
 Microsoft Excel driver が使用されている場合、列名が存在する場合は、最初の行に配置する必要があります。 Microsoft Excel では、"!" 文字を使用する名前を、前に引用符 (') で囲む必要があります。 "!" 文字は "$" 文字に変換されます。これは、名前が逆引用符で囲まれている場合でも、"!" 文字が ODBC 名の中で有効でないためです。 その他の有効な Microsoft Excel 文字 (パイプ文字 (&#124;) を除く) はすべて、列名 (スペースを含む) で使用できます。 Microsoft Excel の列名にスペースを含めるには、区切られた識別子を使用する必要があります。 指定されていない列名は、ドライバーによって生成される名前 (最初の列の "Col1" など) に置き換えられます。  
  
 パイプ文字 (&#124;) は、名前が逆引用符で囲まれているかどうかにかかわらず、列名では使用できません。  
  
 テキストドライバーが使用されている場合、列名が指定されていない場合、ドライバーによって既定の名前が提供されます。 たとえば、ドライバーは、最初の列 F1、2番目の列 F2 などを呼び出します。
