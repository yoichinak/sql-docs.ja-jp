---
description: 複数 hstmts (Paradox ドライバー)
title: 複数の hstmts (Paradox ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 687b87f07142ad23f6faf7155ae974a6d93deab4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449404"
---
# <a name="multiple-hstmts-paradox-driver"></a>複数 hstmts (Paradox ドライバー)
ODBC Paradox ドライバーを使用する場合、テーブルに対して複数の *hstmt* を使用してクエリを実行するには、テーブルに一意のインデックス (Paradox 主キー) が必要です。
