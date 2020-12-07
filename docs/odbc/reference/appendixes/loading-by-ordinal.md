---
description: 序数での読み込み
title: 読み込み (序数 |)Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb8929962e97e7560f50117218f621cd21846fc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429634"
---
# <a name="loading-by-ordinal"></a>序数での読み込み
ODBC 2.x では、序数による読み込みを実行して、接続プロセスのパフォーマンスを向上させることが*できます。* ODBC 2.x ドライバーは、序数が199のダミー関数をエクスポートし *ます* 。ドライバーマネージャーは、これを検出すると、ODBC 関数のアドレスを名前ではなく序数で解決します。 この機能は ODBC 2.x ドライバーでは引き続きサポートされていますが、 *odbc* *3.x ドライバーで*はサポートされていません。
