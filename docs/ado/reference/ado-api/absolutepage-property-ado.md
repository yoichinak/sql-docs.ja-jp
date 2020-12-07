---
description: AbsolutePage プロパティ (ADO)
title: AbsolutePage プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 1d735a8a61d4b62e6fa57427ecbee247d4589040
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977243"
---
# <a name="absolutepage-property-ado"></a>AbsolutePage プロパティ (ADO)
現在のレコードが存在するページを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 32ビットコードの場合、は、1から[レコードセット](./recordset-object-ado.md)オブジェクト ([PageCount](./pagecount-property-ado.md)) 内のページ数までの**Long 型**の値を設定または返します。または、 [positionenum](./positionenum.md)値の1つを返します。  
  
 64ビットコードの場合は、64ビット値を格納するためにに用意されているデータ型を使用します。 たとえば、 **Long 型** の値を使用することも、dbordinal などの64ビットの長さになる別の値を使用することもできます。 **Positionenum**値は、32ビットの長さに制限されているため、使用しないでください。  
  
## <a name="remarks"></a>解説  
 このプロパティは、現在のレコードが配置されているページ番号を識別するために使用できます。 この例では、 [pagesize](./pagesize-property-ado.md) プロパティを使用して、レコード **セット** オブジェクトの合計行セット数を一連のページに論理的に分割しています。各ページには、レコード数が **pagesize** に等しいものが含まれています (最後のページを除き、レコードが少なくなる場合があります)。 このプロパティを使用できるようにするには、プロバイダーが適切な機能をサポートしている必要があります。  
  
-   **AbsolutePage**プロパティを取得または設定するとき、ADO は[AbsolutePosition](./absoluteposition-property-ado.md)プロパティと[PageSize](./pagesize-property-ado.md)プロパティを次のように一緒に使用します。  
  
-   **AbsolutePage**を取得するために、ADO はまず**AbsolutePosition**を取得し、次に**PageSize**で除算します。  
  
-   **AbsolutePage**を設定するために、ADO は**AbsolutePosition**を新しい**AbsolutePage** **値で乗算し、** 値に1を加算します。 その結果、 **AbsolutePage**を正常に設定した後の**レコードセット**内の現在の位置は、そのページの最初のレコードになります。  
  
 **AbsolutePosition**プロパティと同様に、 **AbsolutePage**は1から始まる、現在のレコードが**レコードセット**内の最初のレコードの場合は1になります。 特定のページの最初のレコードに移動するには、このプロパティを設定します。 **PageCount**プロパティから合計ページ数を取得します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [AbsolutePage、PageCount、および PageSize プロパティの例 (VB)](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount、および PageSize プロパティの例 (VC + +)](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition プロパティ (ADO)](./absoluteposition-property-ado.md)   
 [PageCount プロパティ (ADO)](./pagecount-property-ado.md)   
 [PageSize プロパティ (ADO)](./pagesize-property-ado.md)