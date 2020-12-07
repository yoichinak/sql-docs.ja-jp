---
description: マルチスレッド
title: マルチスレッド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 470a3d3a4d76ae038e3c80b9aa9b93dfd1d0ed79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429244"
---
# <a name="multithreading"></a>マルチスレッド
マルチスレッドオペレーティングシステムでは、ドライバーはスレッドセーフである必要があります。 つまり、アプリケーションが複数のスレッドで同じハンドルを使用できるようにする必要があります。 これがどのように実現されるかはドライバーによって異なり、ドライバーは、2つの異なるスレッドで同じハンドルを同時に使用するようにシリアル化します。  
  
 アプリケーションでは、通常、非同期処理ではなく複数のスレッドを使用します。 アプリケーションは、別のスレッドを作成し、そこで ODBC 関数を呼び出して、メインスレッドで処理を続行します。 非同期関数を継続的にポーリングするのではなく、SQL_ATTR_ASYNC_ENABLE statement 属性が使用されている場合と同様に、アプリケーションでは、新しく作成されたスレッドを終了させることができます。  
  
 ステートメントハンドルを受け取り、1つのスレッドで実行されている関数は、別のスレッドから同じステートメントハンドルを使用して **SQLCancel** を呼び出すことによって取り消すことができます。 ドライバーでは、この方法で **SQLCancel** の使用をシリアル化する必要はありませんが、 **SQLCancel** を呼び出すと、他のスレッドで実行されている関数が実際にキャンセルされるという保証はありません。
