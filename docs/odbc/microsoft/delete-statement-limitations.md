---
description: DELETE ステートメントの制限事項
title: DELETE ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b188d782f82e23d031b820bba5f56a30dad414bd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99181589"
---
# <a name="delete-statement-limitations"></a>DELETE ステートメントの制限事項
DELETE ステートメントは、Microsoft Excel またはテキストドライバーではサポートされていません。 Text ドライバーでは INSERT ステートメントがサポートされていることに注意してください。  
  
 DBASE ドライバーでは、"deleted" 値を削除するためのテーブルのパッキングはサポートされていません。  
  
 Paradox ドライバーでテーブルから行を削除するには、テーブルに一意のインデックス (Paradox 主キー) が含まれている必要があります。
