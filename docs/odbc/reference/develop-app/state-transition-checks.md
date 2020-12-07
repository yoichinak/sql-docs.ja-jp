---
description: 状態遷移の確認
title: 状態遷移の確認 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50a845f2b83ada7c9d4f03f252b6d2bc3d3eff3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476374"
---
# <a name="state-transition-checks"></a>状態遷移の確認
ドライバーマネージャーは、環境、接続、またはステートメントの状態が、呼び出される関数に適しているかどうかを確認します。 たとえば、 **SQLConnect** が呼び出されたときに、接続が割り当て済みの状態になっている必要があります。 **Sqlexecute** が呼び出されると、ステートメントは準備済みの状態である必要があります。 ドライバーマネージャーは、状態遷移エラーの SQL_ERROR を返します。
