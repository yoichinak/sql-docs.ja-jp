---
description: Supports メソッド
title: Method | をサポートします。Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a91268668dae9ba430ba696ffb0186749047af9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988323"
---
# <a name="supports-method"></a>Supports メソッド
指定した [レコードセット](./recordset-object-ado.md) オブジェクトが特定の種類の機能をサポートするかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>戻り値  
 *カーソルオプション*引数によって識別されるすべての機能がプロバイダーによってサポートされているかどうかを示す**ブール**値を返します。  
  
#### <a name="parameters"></a>パラメーター  
 *CursorOptions*  
 1つ以上の[カーソルオプションの列挙](./cursoroptionenum.md)値で構成される**Long**式です。  
  
## <a name="remarks"></a>解説  
 **サポート**メソッドを使用して、**レコードセット**オブジェクトがサポートする機能の種類を決定します。 対応する定数が*カーソルオプション*に含まれる機能を**レコードセット**オブジェクトがサポートしている場合、 **supports**メソッドは**True**を返します。 それ以外の場合は **False**を返します。  
  
> [!NOTE]
>  **サポート**メソッドは特定の機能に対して**True**を返す場合がありますが、プロバイダーがすべての状況でこの機能を使用できるようにすることは保証されません。 **サポート**メソッドは、特定の条件が満たされていることを前提として、プロバイダーが指定された機能をサポートできるかどうかを単純に返します。 たとえば、 **サポート** されているメソッドは、カーソルが複数のテーブルの結合に基づいている場合でも、 **レコードセット** オブジェクトが更新をサポートしていることを示している可能性があります。この場合、更新できない列もあります。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Supports メソッドの例 (VB)](./supports-method-example-vb.md)   
 [Supports メソッドの例 (VC + +)](./supports-method-example-vc.md)   
 [CursorType プロパティ (ADO)](./cursortype-property-ado.md)