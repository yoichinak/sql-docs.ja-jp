---
description: UPDATE ステートメントの制限事項
title: UPDATE ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 721af98991f4d63c459ba5df44bc425c245d2dc7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99190623"
---
# <a name="update-statement-limitations"></a>UPDATE ステートメントの制限事項
Paradox ドライバーでテーブルを更新するには、テーブルに一意のインデックス (Paradox 主キー) が必要です。 Borland データベースエンジンを実装せずに Paradox ドライバーを使用する場合、Paradox テーブルを更新することはできません。  
  
 テキストドライバーではサポートされていません。  
  
 Microsoft Excel driver が使用されている場合、値を更新することはできますが、Microsoft Excel スプレッドシートに基づくテーブルから行を削除することはできません。 その結果、UPDATE ステートメントは、Microsoft Excel ドライバーによって正式にサポートされているとは見なされません。 サポートされていると見なされるのは、INSERT ステートメントだけです。
