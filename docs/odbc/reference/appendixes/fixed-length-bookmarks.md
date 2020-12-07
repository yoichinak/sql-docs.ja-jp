---
description: 固定長のブックマーク
title: 固定長のブックマーク |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d357ba96141c658889628941c7f9492db5fd6b66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466178"
---
# <a name="fixed-length-bookmarks"></a>固定長のブックマーク
ODBC *3.x ドライバーが* 固定長のブックマークを使用する odbc 2.x *アプリケーションで* 動作する必要がある場合、ドライバーは次の機能をサポートする必要があります。  
  
-   SQL_USE_BOOKMARKS ステートメントオプションの値として SQL_UB_ON ます。 (SQL_UB_ON は ODBC 3.x では非推奨と *されます*)。  
  
-   SQL_GET_BOOKMARK ステートメントオプション。
