---
description: 算術エラー
title: 算術エラー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2fa142b43f1e96693390f777c90ea6f10705f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500405"
---
# <a name="arithmetic-errors"></a>算術エラー
ODBC ドライバーは、各行をフェッチするときに、SELECT ステートメント内の WHERE 句を評価します。 0除算や数値オーバーフローなどの算術エラーが発生する値が行に含まれている場合、ドライバーはすべての行を返しますが、算術エラーが発生している列に対してはエラーを返します。 ただし、挿入または更新する場合、最初の算術エラーが発生すると、ODBC ドライバーはデータの挿入または更新を停止します。
