---
description: ExtendedAnsiSQL を使用して有効になっているデータの切り捨ての検出
title: ExtendedAnsiSQL | を使用したデータ切り捨て検出の有効化Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26965093caecbc11e94ef738ba6b8ff757b43258
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412892"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>ExtendedAnsiSQL を使用して有効になっているデータの切り捨ての検出
ExtendedAnsiSQL フラグが有効になっていて、アプリケーションが char 列またはバイナリ列にデータを挿入しているときに、データが切り捨てられると、切り捨てが検出されます。 ExtendedAnsiSQL フラグがオフになっている場合、以前のバージョンの ODBC Desktop データベースドライバのように、データは警告なしに切り捨てられます。
