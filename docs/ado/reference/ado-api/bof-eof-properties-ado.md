---
description: BOF、EOF プロパティ (ADO)
title: BOF、EOF プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
author: rothja
ms.author: jroth
ms.openlocfilehash: 710a116e28a102eeac8a7a062a9f66cd8dcbe79c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975783"
---
# <a name="bof-eof-properties-ado"></a>BOF、EOF プロパティ (ADO)
-   **BOF** 現在のレコード位置が、 [レコードセット](./recordset-object-ado.md) オブジェクトの最初のレコードの前にあることを示します。  
  
-   **EOF** 現在のレコード位置が、 **レコードセット** オブジェクトの最後のレコードの後であることを示します。  
  
## <a name="return-value"></a>戻り値  
 **BOF**プロパティと**EOF**プロパティは、**ブール**値を返します。  
  
## <a name="remarks"></a>解説  
 **Recordset**オブジェクトにレコードが含まれているかどうか、またはレコード間の移動時にレコード**セット**オブジェクトの制限を超えていないかどうかを判断するには、 **BOF**プロパティと**EOF**プロパティを使用します。  
  
 **BOF**プロパティは、現在のレコード位置が最初のレコードの前にある場合は**True** (-1) を返し、現在のレコード位置が最初のレコードの前後にある場合は**False** (0) を返します。  
  
 **EOF**プロパティは、現在のレコード位置が最後のレコードの後にある場合は**True**を返し、現在のレコード位置が最後のレコードの前または最後のレコードの前にある場合は**False**を返します。  
  
 **BOF**プロパティまたは**EOF**プロパティのいずれかが**True**の場合、現在のレコードは存在しません。  
  
 レコードを含まない**レコードセット**オブジェクトを開くと、 **BOF**プロパティと**EOF**プロパティが**True**に設定されます (**レコードセット**のこの状態の詳細については、「 [RecordCount](./recordcount-property-ado.md) 」プロパティを参照してください)。 少なくとも1つのレコードを含むレコード **セット** オブジェクトを開くと、最初のレコードが現在のレコードになり、 **BOF** プロパティと **EOF** プロパティは **False**になります。  
  
 **Recordset**オブジェクト内の最後のレコードを削除すると、現在のレコードの位置を変更しようとしたときに、 **BOF**プロパティと**EOF**プロパティが**False**のままになる場合があります。  
  
 次の表は、 **BOF**プロパティと**EOF**プロパティのさまざまな組み合わせで許可される**移動**方法を示しています。  
  
||MoveFirst<br /><br /> MoveLast|MovePrevious<br /><br /> < 0 に移動|0の移動|MoveNext<br /><br /> > 0 に移動|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF** =**True**、 **EOF** = **False**|許可|エラー|エラー|許可|  
|**BOF** =**False**、 **EOF** = **True**|許可|許可|エラー|エラー|  
|両方 **True**|エラー|エラー|エラー|エラー|  
|両方 **False**|許可|許可|許可|許可|  
  
 **Move**メソッドを許可しても、メソッドがレコードを正常に見つけることは保証されません。これは、指定された**Move**メソッドを呼び出すことによってエラーが生成されないことを意味します。  
  
 次の表は、さまざまな**Move**メソッドを呼び出してもレコードを正常に見つけることができない場合に、 **BOF**プロパティと**EOF**プロパティの設定がどのように行われるかを示しています。  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**、 **MoveLast**|**True**に設定|**True**に設定|  
|0の**移動**|変更なし|変更なし|  
|**MovePrevious**、 **移動** < 0|**True**に設定|変更なし|  
|**MoveNext**、 **移動** > 0|変更なし|**True**に設定|  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [BOF、EOF、および Bookmark プロパティの例 (VB)](./bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、EOF、および Bookmark プロパティの例 (VC + +)](./bof-eof-and-bookmark-properties-example-vc.md)