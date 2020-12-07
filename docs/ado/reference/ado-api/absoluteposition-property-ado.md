---
description: AbsolutePosition プロパティ (ADO)
title: AbsolutePosition プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ecb3290d73032568af7e0a92baf0c9d1b2628f4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977161"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition プロパティ (ADO)
[レコードセット](./recordset-object-ado.md)オブジェクトの現在のレコードの位置を表す序数を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 32ビットコードの場合、は、1から**レコードセット**オブジェクト ([RecordCount](./recordcount-property-ado.md)) のレコード数までの**Long 型**の値を設定または返します。または、 [positionenum](./positionenum.md)値の1つを返します。  
  
 64ビットコードの場合は、64ビット値を格納するためにに用意されているデータ型を使用します。 たとえば、Long または DBORDINAL などの64ビット長の別の値を使用することができます。 **Positionenum**値は、32ビットの長さに制限されているため、使用しないでください。  
  
## <a name="remarks"></a>解説  
 ADO では、 **AbsolutePosition** プロパティを設定するために、使用している OLE DB プロバイダーが [IRowsetLocate: IRowset](/previous-versions/windows/desktop/ms721190(v=vs.85)) インターフェイスを実装する必要があります。  
  
 順方向専用カーソルまたは動的カーソルで開かれた**レコードセット**の**AbsolutePosition**プロパティにアクセスすると、エラー **adErrFeatureNotAvailable**が発生します。 その他の種類のカーソルでは、OLE DB プロバイダーが **IRowsetScroll: IRowsetLocate** インターフェイスをサポートしている限り、正しい位置が返されます。 プロバイダーで **IRowsetScroll** インターフェイスがサポートされていない場合、プロパティは **adposunknown**に設定されます。 **IRowsetScroll**がサポートされているかどうかを判断するには、プロバイダーのドキュメントを参照してください。  
  
 **AbsolutePosition**プロパティを使用して、レコード**セット**オブジェクトの序数位置に基づいてレコードに移動するか、現在のレコードの序数位置を決定します。 このプロパティを使用できるようにするには、プロバイダーが適切な機能をサポートしている必要があります。  
  
 [AbsolutePage](./absolutepage-property-ado.md)プロパティと同様に、 **AbsolutePosition**は1から始まる、現在のレコードが**レコードセット**内の最初のレコードの場合は1になります。 レコード **セット** オブジェクト内のレコードの合計数は、 [RecordCount](./recordcount-property-ado.md) プロパティから取得できます。  
  
 **AbsolutePosition**プロパティを設定すると、現在のキャッシュ内のレコードの場合でも、ADO は、指定したレコードで始まる新しいレコードのグループを使用してキャッシュを再読み込みします。 このグループのサイズは、 [CacheSize](./cachesize-property-ado.md) プロパティによって決定されます。  
  
> [!NOTE]
>  **AbsolutePosition**プロパティは、サロゲートレコード番号として使用しないでください。 前のレコードを削除すると、特定のレコードの位置が変更されます。 また、**レコードセット**オブジェクトが再クエリまたは再度開かれた場合、特定のレコードの**AbsolutePosition**が同じであることは保証されません。 ブックマークは、特定の位置を保持して返すための推奨される方法であり、すべての種類の **レコードセット** オブジェクトに対して配置する唯一の方法です。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [AbsolutePosition およびカーソルのプロパティの例 (VB)](./absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition およびカーソルのプロパティの例 (VC + +)](./absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage プロパティ (ADO)](./absolutepage-property-ado.md)   
 [RecordCount プロパティ (ADO)](./recordcount-property-ado.md)