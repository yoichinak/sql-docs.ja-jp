---
description: 記述子ハンドルの取得
title: 記述子ハンドルの取得 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c46ce0bff7240c121c6c56a5c3cd1b19769afb04
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429204"
---
# <a name="obtaining-descriptor-handles"></a>記述子ハンドルの取得
アプリケーションは、明示的に割り当てられた記述子のハンドルを、 **SQLAllocHandle**への呼び出しの出力引数として取得します。 暗黙的に割り当てられた記述子のハンドルは、 **SQLGetStmtAttr**を呼び出すことによって取得されます。
