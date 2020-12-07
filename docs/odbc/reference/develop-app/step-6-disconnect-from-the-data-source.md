---
description: 手順 6:データ ソースから切断する
title: '手順 6: データソースからの切断 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06b3b50653578388ca3d4e20b598f63879f38e88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461344"
---
# <a name="step-6-disconnect-from-the-data-source"></a>手順 6:データ ソースから切断する
最後の手順は、次の図に示すように、データソースから切断することです。 まず、アプリケーションは **Sqlfreehandle**を呼び出して、ステートメントハンドルを解放します。 詳細については、「 [ステートメントハンドルを解放する](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)」を参照してください。  
  
 ![データ ソースからの切断の表示](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 次に、アプリケーションは **Sqldisconnect** を使用してデータソースから切断し、 **sqlfreehandle**を使用して接続ハンドルを解放します。 詳細については、「 [データソースまたはドライバーからの切断](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)」を参照してください。  
  
 最後に、アプリケーションは **Sqlfreehandle** を使用して環境ハンドルを解放し、ドライバーマネージャーをアンロードします。 詳細については、「 [環境ハンドルの割り当て](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)」を参照してください。
