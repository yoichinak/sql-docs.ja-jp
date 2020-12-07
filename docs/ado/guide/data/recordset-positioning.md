---
description: レコードセットを配置する
title: レコードセットの配置 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: rothja
ms.author: jroth
ms.openlocfilehash: 1f97f5b9c9a947362edffaa88f878c96d63b270f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979883"
---
# <a name="recordset-positioning"></a>レコードセットを配置する
**AbsolutePosition**プロパティを使用して、レコード**セット**オブジェクトの序数位置に基づいてレコードに移動するか、現在のレコードの位置を表す序数を指定します。 このプロパティを使用できるようにするには、プロバイダーが適切な機能をサポートしている必要があります。  
  
 **AbsolutePosition** は1から始まる、現在のレコードが **レコードセット**内の最初のレコードの場合は1になります。 前述のように、 **RecordCount**プロパティから、レコード**セット**オブジェクト内のレコードの合計数を取得できます。  
  
 **AbsolutePosition**プロパティを設定すると、現在のキャッシュ内のレコードの場合でも、ADO は、指定したレコードで始まる新しいレコードのグループを使用してキャッシュを再読み込みします。 このグループのサイズは、 **CacheSize** プロパティによって決定されます。  
  
> [!NOTE]
>  **AbsolutePosition**プロパティは、サロゲートレコード番号として使用しないでください。 前のレコードを削除すると、特定のレコードの位置が変更されます。 また、**レコードセット**オブジェクトが再クエリまたは再度開かれた場合、特定のレコードの**AbsolutePosition**が同じであることは保証されません。 ブックマークは、特定の位置を保持して返す場合に推奨される方法であり、すべての種類の **レコードセット** オブジェクトに対して配置する唯一の方法です。
