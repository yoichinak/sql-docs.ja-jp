---
description: ブックマークの比較
title: ブックマークの比較 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 939c3780fc9c6738a307e9a969a346951cfac5e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476784"
---
# <a name="comparing-bookmarks"></a>ブックマークの比較
ブックマークはバイト比較可能であるため、等価性または非等値を比較できます。 これを行うために、アプリケーションは各ブックマークをバイトの配列として扱い、2つのブックマークを1バイトずつ比較します。 ブックマークは、結果セット内でのみ一意であることが保証されるため、異なる結果セットから取得されたブックマークを比較することは意味がありません。
