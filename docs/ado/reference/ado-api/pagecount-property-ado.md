---
description: PageCount プロパティ (ADO)
title: PageCount プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
author: rothja
ms.author: jroth
ms.openlocfilehash: 07eb8ef6a51b67b70b1a0bd4b8fecba116df58a4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166927"
---
# <a name="pagecount-property-ado"></a>PageCount プロパティ (ADO)
[Recordset](./recordset-object-ado.md)オブジェクトに格納されているデータのページ数を示します。  
  
## <a name="return-value"></a>戻り値  
 **レコードセット** 内のページ数を示す **Long 型** の値を返します。  
  
## <a name="remarks"></a>コメント  
 **PageCount** プロパティを使用して、**レコードセット** オブジェクトに含まれるデータのページ数を確認します。 *ページ* は、サイズが [PageSize](./pagesize-property-ado.md) プロパティ設定と等しいレコードのグループです。 **PageSize** 値よりも少数のレコードがあるため、最後のページが不完全な場合でも、 **PageCount** 値の追加ページとしてカウントされます。 **Recordset** オブジェクトがこのプロパティをサポートしていない場合、 **PageCount** がわからないであることを示すために、値は-1 になります。  
  
 ページ機能の詳細については、「 **PageSize** プロパティと [AbsolutePage](./absolutepage-property-ado.md) プロパティ」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [AbsolutePage、PageCount、および PageSize プロパティの例 (VB)](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount、および PageSize プロパティの例 (VC + +)](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage プロパティ (ADO)](./absolutepage-property-ado.md)   
 [PageSize プロパティ (ADO)](./pagesize-property-ado.md)   
 [RecordCount プロパティ (ADO)](./recordcount-property-ado.md)