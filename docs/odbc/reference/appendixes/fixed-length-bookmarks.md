---
description: 固定長のブックマーク
title: Fixed-Length ブックマーク |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d5eb7acd97a83be0d150cec8b19a5a3e25a7bf6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99194803"
---
# <a name="fixed-length-bookmarks"></a>固定長のブックマーク
ODBC *3.x ドライバーが* 固定長のブックマークを使用する odbc 2.x *アプリケーションで* 動作する必要がある場合、ドライバーは次の機能をサポートする必要があります。  
  
-   SQL_USE_BOOKMARKS ステートメントオプションの値として SQL_UB_ON ます。 (SQL_UB_ON は ODBC 3.x では非推奨と *されます*)。  
  
-   SQL_GET_BOOKMARK ステートメントオプション。
