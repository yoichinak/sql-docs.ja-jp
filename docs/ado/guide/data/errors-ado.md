---
description: エラー (ADO)
title: エラー (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 8ae6611b-3069-4155-b014-c0c9da37be39
author: rothja
ms.author: jroth
ms.openlocfilehash: e779d6b0aac1e48f64d9544eda0c064f7278c496
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991313"
---
# <a name="errors-ado"></a>エラー (ADO)
ADO オブジェクトに関連する操作では、1つ以上のプロバイダーエラーが発生することがあります。 各エラーが発生すると、**接続**オブジェクトの**エラー**コレクションに1つまたは複数の**エラー**オブジェクトが配置されます。 ADO アプリケーションでの警告とエラーの処理の詳細については、「 [エラー処理](./error-handling.md)」を参照してください。  
  
 アプリケーションエラーは、別のメカニズムを使用して発生させることができます。 たとえば、Visual Basic では、 **Err** オブジェクトにアプリケーションレベルのエラーが含まれます。