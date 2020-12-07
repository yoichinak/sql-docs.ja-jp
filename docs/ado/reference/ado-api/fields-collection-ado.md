---
description: Fields コレクション (ADO)
title: Fields コレクション (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f16fd27e7bee9d3f9e922de4db625b897266a61
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973123"
---
# <a name="fields-collection-ado"></a>Fields コレクション (ADO)
[レコードセット](./recordset-object-ado.md)または[レコード](./record-object-ado.md)オブジェクトのすべての[フィールド](./field-object.md)オブジェクトを格納します。  
  
## <a name="remarks"></a>解説  
 **レコードセット**オブジェクトには、 **Field**オブジェクトで構成された**フィールド**コレクションがあります。 各 **Field** オブジェクトは、 **レコードセット**内の列に対応します。 コレクションの[Refresh](./refresh-method-ado.md)メソッドを呼び出すことによって、**レコードセット**を開く前に**フィールド**コレクションを設定できます。  
  
> [!NOTE]
>  **Field**オブジェクトの使用方法の詳細については、「 **field**オブジェクト」を参照してください。  
  
 **Fields**コレクションには、仮メソッドがあります。[このメソッドは](./append-method-ado.md)、**フィールド**オブジェクトを作成し、コレクションに追加し、 **Update**メソッドを使用して、追加または削除を終了します。  
  
 **レコード**オブジェクトには、2つの特殊なフィールドがあります。これらのフィールドには、定数定数を使用[してインデックス](./fieldenum.md)を作成できます。 一方の定数は、 **レコード**の既定のストリームを格納しているフィールドにアクセスします。もう1つの定数は、 **レコード**の絶対 URL 文字列を含むフィールドにアクセスします。  
  
 特定のプロバイダー (たとえば、 [Microsoft OLE DB Provider For Internet Publishing](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) では、**レコード**または**レコードセット**に使用できるフィールドのサブセットを**フィールド**コレクションに設定できます。 その他のフィールドは、名前によって最初に参照されるか、コードによってインデックスが作成されるまで、コレクションに追加されません。  
  
 存在しないフィールドを名前で参照しようとすると、 **Adfieldpendinginsert**という[状態](./status-property-ado-field.md)の**フィールドコレクションに**新しい**フィールド**オブジェクトが追加されます。 [Update](./update-method.md)を呼び出すと、プロバイダーで許可されている場合、ADO によってデータソースに新しいフィールドが作成されます。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Fields コレクションのプロパティ、メソッド、およびイベント](./fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Field オブジェクト](./field-object.md)