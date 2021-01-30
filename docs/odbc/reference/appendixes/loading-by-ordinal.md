---
description: 序数での読み込み
title: 読み込み (序数 |)Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ffb2516a79144a5ae79b21e6621882056b1f69ff
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99184375"
---
# <a name="loading-by-ordinal"></a>序数での読み込み
ODBC 2.x では、序数による読み込みを実行して、接続プロセスのパフォーマンスを向上させることが *できます。* ODBC 2.x ドライバーは、序数が199のダミー関数をエクスポートし *ます* 。ドライバーマネージャーは、これを検出すると、ODBC 関数のアドレスを名前ではなく序数で解決します。 この機能は ODBC 2.x ドライバーでは引き続きサポートされていますが、 *odbc* *3.x ドライバーで* はサポートされていません。
