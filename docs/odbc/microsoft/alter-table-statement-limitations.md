---
description: ALTER TABLE ステートメントの制限事項
title: ALTER TABLE ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53f86e8d2c21fb6ea2d016610848773564d4a384
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449594"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE ステートメントの制限事項
DBASE または Paradox ドライバーを使用する場合、インデックスが作成され、新しいレコードが追加されると、インデックスが削除され、テーブルの内容が削除されない限り、ALTER TABLE ステートメントでテーブルの構造を変更することはできません。  
  
 Microsoft Excel またはテキストドライバーでは、ALTER TABLE ステートメントはサポートされていません。  
  
> [!NOTE]  
>  Borland データベースエンジンを実装せずに Paradox ドライバーを使用する場合、ALTER TABLE ステートメントはサポートされません。read ステートメントと append ステートメントのみが許可されます。
