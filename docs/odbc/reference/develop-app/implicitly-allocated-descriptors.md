---
description: 暗黙的に割り当てられた記述子
title: 暗黙的に割り当てられた記述子 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5daa7f622798e1394c186b333069933b48e367af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461424"
---
# <a name="implicitly-allocated-descriptors"></a>暗黙的に割り当てられた記述子
ステートメントハンドルが割り当てられると、アプリケーションは、4つの記述子のセットを暗黙的に割り当てます。 アプリケーションは、暗黙的に割り当てられたこれらの記述子のハンドルを、ステートメントハンドルの属性として取得できます。 アプリケーションがステートメントハンドルを解放すると、ドライバーはそのハンドルで暗黙的に割り当てられたすべての記述子を解放します。
