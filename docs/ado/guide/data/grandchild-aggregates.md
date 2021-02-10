---
description: 孫の集計
title: 孫集計 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
author: rothja
ms.author: jroth
ms.openlocfilehash: a5cae4f996112d660564cb8efd3ea9b7e53c4f9f
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100033152"
---
# <a name="grandchild-aggregates"></a>孫の集計
Shape コマンドの句で作成されたチャプター列には、 *章エイリアス名* (通常は AS キーワードを使用) が指定されている場合があります。 列を含む子を識別する完全修飾名を使用して、整形された **レコードセット** の任意のチャプター内の任意の列を識別できます。 たとえば、親章 chap1 に、amount 列を含む chap2 という子のチャプターが含まれている場合、修飾名は chap1 になります。修飾名は、集計関数 (SUM、AVG、MAX、MIN、COUNT、STDEV、ANY) のいずれかの引数として使用できます。  
  
## <a name="see-also"></a>参照  
 [データ シェイプの例](./data-shaping-example.md)