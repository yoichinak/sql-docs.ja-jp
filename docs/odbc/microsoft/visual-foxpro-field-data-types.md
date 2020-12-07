---
description: Visual FoxPro フィールドのデータ型
title: Visual FoxPro フィールドのデータ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 65410f16367af8764e8572c58e53831f3f7b9cda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449054"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro フィールドのデータ型
次の表に、ALTER TABLE と CREATE TABLE の *FieldType* 引数の値を示し、 *Nfieldwidth* 引数と *nprecision* 引数が必要かどうかを示します。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|説明|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|幅*n*の文字フィールド|  
|D|-|-|Date|  
|F|N|d|*小数点以下を*含む幅*n*の浮動小数点数値フィールド|  
|G|-|-|全般|  
|I|-|-|Integer|  
|L|-|-|論理|  
|M|-|-|メモ|  
|N|N|d|*D*小数点以下を含む幅*n*の数値フィールド|  
|T|-|-|DateTime|  
|Y|-|-|Currency|
