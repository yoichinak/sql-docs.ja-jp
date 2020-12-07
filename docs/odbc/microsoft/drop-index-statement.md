---
description: DROP INDEX ステートメント
title: DROP INDEX Statement |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DROP INDEX [ODBC]
- SQL grammar [ODBC], DROP INDEX
ms.assetid: cd0ff767-9254-413b-bd1a-bed26c6774f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01b0c51d3fff15184b4542299c97423fbed15aa3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412678"
---
# <a name="drop-index-statement"></a>DROP INDEX ステートメント
Microsoft Access、dBASE、または Paradox ドライバーが使用されている場合、DROP INDEX ステートメントの構文は "DROP INDEX a on b" になります。ここで、"a" はインデックスの名前、"b" はテーブルの名前 (DROP INDEX *インデックス名*ではありません) です。  
  
 Paradox ドライバーを使用すると、DROP INDEX ステートメントによって、Paradox セカンダリインデックスファイルが削除されます。  
  
 DROP INDEX ステートメントは、Microsoft Excel またはテキストドライバーではサポートされていません。
