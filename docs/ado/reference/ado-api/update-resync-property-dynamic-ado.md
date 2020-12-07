---
description: Update Resync プロパティ - 動的 (ADO)
title: 更新の再同期プロパティ-動的 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: rothja
ms.author: jroth
ms.openlocfilehash: 506fd7fecee179a055e23ffad1beab76bcd2fbe2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988093"
---
# <a name="update-resync-property-dynamic-ado"></a>Update Resync プロパティ - 動的 (ADO)
[UpdateBatch](./updatebatch-method.md)メソッドの後に暗黙の再[同期](./resync-method.md)メソッド操作を実行するかどうかを指定します。それを行う場合は、その操作のスコープを指定します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 1つ以上の [ADCPROP_UPDATERESYNC_ENUM](./adcprop-updateresync-enum.md) 値を設定または返します。  
  
## <a name="remarks"></a>解説  
 ADCPROP_UPDATERESYNC_ENUM の値は、他の値の組み合わせを既に表している adResyncAll を除き、組み合わせて使用できます。  
  
 定数 **adResyncConflicts** は、再同期値を基になる値として格納しますが、保留中の変更はオーバーライドしません。  
  
 **更新**の再同期は、[カーソルの場所](./cursorlocation-property-ado.md)プロパティが**adUseClient**に設定されている場合に、[レコードセット](./recordset-object-ado.md)オブジェクトの[プロパティ](./properties-collection-ado.md)コレクションに追加される動的プロパティです。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)