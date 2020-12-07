---
description: 環境ハンドル
title: 環境ハンドル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa22a89288f4dd5a8400484078f57b60fc135fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461504"
---
# <a name="environment-handles"></a>環境ハンドル
*環境*とは、データにアクセスするためのグローバルなコンテキストです。環境に関連付けられている情報は、次のように、本質的にグローバルな情報です。  
  
-   環境の状態  
  
-   現在の環境レベルの診断  
  
-   環境で現在割り当てられている接続のハンドル  
  
-   各環境属性の現在の設定  
  
 ODBC (ドライバーマネージャーまたはドライバー) を実装するコード内では、この情報を格納する構造体が環境ハンドルによって識別されます。  
  
 ODBC アプリケーションでは、環境ハンドルは頻繁には使用されません。 これらは、 **Sqldatasources ソース** および **sqldatasources** の呼び出しで常に使用され、 **SQLAllocHandle**、 **SQLEndTran**、 **sqlfreehandle**、 **SQLGetDiagField**、 **SQLGetDiagRec**の呼び出しで使用されることがあります。  
  
 ODBC (ドライバーマネージャーまたはドライバー) を実装するコードの各部分には、1つまたは複数の環境ハンドルが含まれています。 たとえば、ドライバーマネージャーは、接続されているアプリケーションごとに個別の環境ハンドルを保持します。 環境ハンドルは **SQLAllocHandle** で割り当てられ、 **sqlfreehandle**と共に解放されます。
