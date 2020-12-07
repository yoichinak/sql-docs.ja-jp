---
description: Status プロパティ (ADO Field)
title: Status プロパティ (ADO Field) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
author: rothja
ms.author: jroth
ms.openlocfilehash: 11f59e99eab0a742a4d7618f7ac66cb486af2933
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988723"
---
# <a name="status-property-ado-field"></a>Status プロパティ (ADO Field)
[フィールド](./field-object.md)オブジェクトの状態を示します。  
  
## <a name="return-value"></a>戻り値  
 [Fieldstatusenum](./fieldstatusenum.md)値を返します。 既定値は **adFieldOK**です。  
  
## <a name="remarks"></a>解説  
  
## <a name="record-field-status"></a>レコードフィールドの状態  
 [Record](./record-object-ado.md)オブジェクトの Fields コレクション内の**Field**オブジェクトの値に対する変更は、オブジェクトの[Update](./update-method.md)メソッドが呼び出されるまでキャッシュされます。 その時点で、フィールドの値の変更によってエラーが発生した場合、OLE DB によってエラー **DB_E_ERRORSOCCURRED** (2147749409) が発生します。 エラーの原因となった**フィールド**コレクション内のいずれかの**フィールド**オブジェクトの Status プロパティには、問題の原因を説明する[fieldstatusenum](./fieldstatusenum.md)の値が含まれます。  
  
 パフォーマンスを向上させるために、**レコード**オブジェクトの[フィールド](./fields-collection-ado.md)コレクションへの追加と削除は、 **Update**メソッドが呼び出されるまでキャッシュされます。その後、バッチオプティミスティック更新で変更が行われます。 **Update**メソッドが呼び出されていない場合、サーバーは更新されません。 更新が失敗した場合は、OLE DB プロバイダエラー (DB_E_ERRORSOCCURRED) が返され、 **status** プロパティは操作とエラーステータスコードの組み合わせた値を示します。 たとえば、 **Adfieldpendinginsert または Adfieldpendinginsert が拒否**されました。 各**フィールド**の**Status**プロパティを使用して、**フィールド**が追加、変更、または削除されなかった理由を判断できます。  
  
 **フィールド**を追加、変更、または削除するときに発生する問題の多くは、 **Status**プロパティを通じて報告されます。 たとえば、ユーザーが **フィールド**を削除すると、フィールドコレクションから削除対象 **として** マークされます。 ユーザーがアクセス許可のない**フィールド**を削除しようとしたために、後続の**更新**でエラーが返された場合、**フィールド**の**状態**は**adfieldpermissiondenied または adfieldpendingdelete**になります。 [CancelUpdate](./cancelupdate-method-ado.md)メソッドを呼び出すと、元の値が復元され、**状態**が**adFieldOK**に設定されます。  
  
 同様に、新しい**フィールド**が追加され、不適切な値が指定されたため、 **Update**メソッドはエラーを返す場合があります。 この場合、新しい **フィールド** は **フィールド** コレクションに含まれ、 **adfieldpendinginsert** の状態と、おそらく (プロバイダーに応じて) **adfieldcantcreate** の状態になります。 新しい **フィールド** に適切な値を指定し、もう一度 **Update** を呼び出します。  
  
## <a name="recordset-field-status"></a>レコードセットフィールドの状態  
 [レコードセット](./recordset-object-ado.md)の Fields コレクション内の**Field**オブジェクトの値に対する変更は、オブジェクトの[Update](./update-method.md)メソッドが呼び出されるまでキャッシュされます。 その時点で、フィールドの値の変更によってエラーが発生した場合、OLE DB によってエラー **DB_E_ERRORSOCCURRED** (2147749409) が発生します。 エラーの原因となった**フィールド**コレクション内のいずれかの**フィールド**オブジェクトの Status プロパティには、問題の原因を説明する[fieldstatusenum](./fieldstatusenum.md)の値が含まれます。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](./field-object.md)  
  
## <a name="see-also"></a>参照  
 [Status プロパティの例 (Field) (VB)](./status-property-example-field-vb.md)   
 [Status プロパティの例 (VC++)](./status-property-example-vc.md)