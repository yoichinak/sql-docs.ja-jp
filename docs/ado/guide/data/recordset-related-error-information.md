---
description: レコードセット関連のエラー情報
title: レコードセット関連のエラー情報 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: rothja
ms.author: jroth
ms.openlocfilehash: 454c62b969ee69e6186792ce77873c8c8fbb5704
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979813"
---
# <a name="recordset-related-error-information"></a>レコードセット関連のエラー情報
バッチ処理中 **、レコードセットオブジェクトの** **Status**プロパティは、レコード**セット**内の個々のレコードに関する情報を提供します。 バッチの更新が行われる前に、レコード**セット**の**Status**プロパティには、追加、変更、および削除するレコードに関する情報が反映されます。 **UpdateBatch**が呼び出された後、 **Status**プロパティは操作が成功したか失敗したかを示します。 レコード **セット**内のレコードに移動すると、[ **状態** ] プロパティの値が、現在のレコードの状態を示すように変更されます。
