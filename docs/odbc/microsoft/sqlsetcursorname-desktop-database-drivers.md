---
description: SQLSetCursorName (デスクトップ データベース ドライバー)
title: SQLSetCursorName (デスクトップデータベースドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14fe15c6cdbdf50e6d28ca7e9a1168f54626e83b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411557"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (デスクトップ データベース ドライバー)
ドライバーは位置指定更新をサポートしておらず、WHERE CURRENT OF *カーソル名* 構文による削除をサポートしていないため、 **SQLSetCursorName** はサポートされていますが、位置指定更新には使用できません。 カーソルライブラリが有効になっていて、アプリケーションが **SQLExtendedFetch**を使用している場合にのみ使用できます。
