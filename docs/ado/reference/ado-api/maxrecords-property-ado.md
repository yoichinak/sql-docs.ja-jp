---
description: MaxRecords プロパティ (ADO)
title: MaxRecords プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
author: rothja
ms.author: jroth
ms.openlocfilehash: 31870c4df71b20c162f95f1f1d942dde63885227
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990643"
---
# <a name="maxrecords-property-ado"></a>MaxRecords プロパティ (ADO)
クエリから [レコードセット](./recordset-object-ado.md) に返されるレコードの最大数を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 返されるレコードの最大数を示す **Long 型** の値を設定または返します。 既定値はゼロ (**0**) です。これは制限がないことを意味します。  
  
## <a name="remarks"></a>解説  
 データソースからプロバイダーが返すレコードの数を制限するには、 **MaxRecords** プロパティを使用します。 このプロパティの既定の設定は0です。これは、プロバイダーが要求されたすべてのレコードを返すことを意味します。  
  
 レコードセットが開いている場合は、**レコードセット**が閉じられ、読み取り専用になっている場合、 **MaxRecords**プロパティは読み取り/書き込み可能です。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [MaxRecords プロパティの例 (VB)](./maxrecords-property-example-vb.md)   
 [MaxRecords プロパティの例 (VC++)](./maxrecords-property-example-vc.md)