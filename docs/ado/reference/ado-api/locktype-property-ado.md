---
description: LockType プロパティ (ADO)
title: LockType プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
author: rothja
ms.author: jroth
ms.openlocfilehash: 74e86b054ac9d63527cc0f142ee50aa81acbe4b4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990693"
---
# <a name="locktype-property-ado"></a>LockType プロパティ (ADO)
編集中にレコードに配置されたロックの種類を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 [Locktypeenum](./locktypeenum.md)値を設定または返します。 既定値は **Adlockreadonly**です。  
  
## <a name="remarks"></a>解説  
 [レコードセット](./recordset-object-ado.md)を開く前に、 **LockType**プロパティを設定して、プロバイダーが使用するロックの種類を指定します。 開いている **レコードセット** オブジェクトで使用中のロックの種類を返すには、プロパティを読み取ります。  
  
 プロバイダーは、すべてのロックの種類をサポートしているとは限りません。 プロバイダーが要求された **LockType** 設定をサポートできない場合は、別の種類のロックに置き換えられます。 **レコードセット**オブジェクトで使用できる実際のロック機能を確認するには、 **Adupdate**と**adupdate**の[サポート](./supports-method.md)メソッドを使用します。  
  
 [カーソル位置](./cursorlocation-property-ado.md)プロパティが**adUseClient**に設定されている場合、 **adlockpessimistic**設定はサポートされません。 サポートされていない値が設定されている場合、エラーは発生しません。サポートされている最も近い **LockType** が代わりに使用されます。  
  
 **LockType**プロパティは、レコードセットが閉じられている場合は読み取り/書き込みが可能で、**レコードセット**が開いている場合は読み取り専用です。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況** クライアント側の **レコードセット** オブジェクトで使用する場合、 **LockType** プロパティは **adlockbatchoptimistic**にのみ設定できます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [CursorType、LockType、および EditMode プロパティの例 (VB)](./cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType、および EditMode プロパティの例 (VC + +)](./cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch メソッド (ADO)](./cancelbatch-method-ado.md)   
 [UpdateBatch メソッド](./updatebatch-method.md)