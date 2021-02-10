---
description: データを確認するためのサンプルのレコードセット
title: データを検査するためのサンプルレコードセットMicrosoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: rothja
ms.author: jroth
ms.openlocfilehash: baea4d79057a46ec26c6ccd82f834f5fa3481091
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037072"
---
# <a name="sample-recordset-for-examining-data"></a>データを確認するためのサンプルのレコードセット
まず、Microsoft SQL Server で Northwind サンプルデータベースに対して実行される、次の SQL クエリを使用して返された **レコードセット** オブジェクトを見てみましょう。  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 結果の **レコードセット** オブジェクトには、次の表に示すように、データベースで生成されたすべてのが含まれます。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|あなた Bob's 有機理屈 Pears|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle ラウト|45.6000|  
|51|Manjimup 理屈リンゴ|53.0000|  
|74|Longlife Tofu|10.0000|  
  
 これらの結果を自分で取得することに関心がある場合は、次の JScript の例を試してください。  
  
-   [レコードセットを返す JScript の例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
