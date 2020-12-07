---
description: データ型の制限事項
title: データ型の制限 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4853846f21aa0ad763295bbdc4233c472ac53864
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412788"
---
# <a name="data-type-limitations"></a>データ型の制限事項
Microsoft ODBC Desktop データベースドライバーでは、データ型に次の制限が適用されます。  
  
|データ型|説明|  
|---------------|-----------------|  
|すべてのデータ型|型変換エラーが発生すると、影響を受ける列が NULL に設定される可能性があります。|  
|BINARY|長さ0のバイナリ列を作成すると、実際には255バイトのバイナリ列が返されます。|  
|DATE|CONVERT 関数では、DATE データ型を別のデータ型 (またはそれ自体) に変換することはできません。|  
|DECIMAL (真数)|サポートされていません。|  
|浮動小数点データ型|浮動小数点数の小数点以下の桁数は、Windows のコントロールパネルの [インターナショナル] セクションで設定した数値形式によって制限される場合があります。|  
|NUMERIC|最大有効桁数と28の小数点以下桁数をサポートします。|  
|timestamp|TIMESTAMP データ型は、CONVERT 関数によってそれ自体に変換することはできません。|  
|TINYINT|TINYINT 値は常に符号なしです。|  
|長さ0の文字列|DBASE、Microsoft Excel、Paradox、または Textdriver を使用するときに、長さ0の文字列を列に挿入すると、実際には NULL が挿入されます。|
