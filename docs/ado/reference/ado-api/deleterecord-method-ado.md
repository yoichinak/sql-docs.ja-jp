---
description: DeleteRecord メソッド (ADO)
title: DeleteRecord メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
author: rothja
ms.author: jroth
ms.openlocfilehash: 634e28fb1bcc6d246de72164f33d3d252f63505a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974003"
---
# <a name="deleterecord-method-ado"></a>DeleteRecord メソッド (ADO)
[レコード](../../../ado/reference/ado-api/record-object-ado.md)によって表されるエンティティを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 省略可能。 削除するエンティティ (ファイルやディレクトリなど) を識別する URL を含む **文字列** 値です。 *Source*を省略した場合、または空の文字列を指定した場合は、現在の[レコード](../../../ado/reference/ado-api/record-object-ado.md)によって表されるエンティティが削除されます。 レコードがコレクションレコード (ディレクトリなどの**Adcollectionrecord**の[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) ) である場合は、すべての子 (サブディレクトリなど) も削除されます。  
  
 *非同期*  
 省略可能。 **ブール**値。 **True**の場合、削除操作が非同期であることを指定します。  
  
## <a name="remarks"></a>解説  
 このメソッドの完了後に、この **レコード** によって表されるオブジェクトに対する操作が失敗する可能性があります。 **DeleteRecord**を呼び出した後は、レコードがデータソースで**レコード**を更新するタイミングによってはレコードの動作が予測不能に**なる可能性が**あるため、**レコード**を閉じる必要があります。  
  
 この **レコード** が [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)から取得された場合、この操作の結果は **レコードセット**にすぐには反映されません。 レコードセットを閉じて再度開くか、**レコードセットの** [Requery](../../../ado/reference/ado-api/requery-method.md)メソッド、 [Update](../../../ado/reference/ado-api/update-method.md)メソッド、または[Resync](../../../ado/reference/ado-api/resync-method.md)メソッドを実行して、**レコードセット**を更新します。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../../ado/guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Delete メソッド (ADO Fields コレクション)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete メソッド (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
