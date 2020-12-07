---
description: CursorOptionEnum
title: カーソルオプションの列挙 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
author: rothja
ms.author: jroth
ms.openlocfilehash: a14102f57f2b328314e20e4124ca7e78258fb7e0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974353"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
[サポート](./supports-method.md)メソッドがテストする必要がある機能を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|では、 [AddNew](./addnew-method-ado.md) メソッドをサポートして、新しいレコードを追加します。|  
|**adApproxPosition**|0x4000|では、 [AbsolutePosition](./absoluteposition-property-ado.md) プロパティと [AbsolutePage](./absolutepage-property-ado.md) プロパティがサポートされています。|  
|**adBookmark**|0x2000|は、 [Bookmark](./bookmark-property-ado.md) プロパティをサポートして、特定のレコードにアクセスできるようにします。|  
|**adDelete**|0x1000800|レコードを削除するための [delete](./delete-method-ado-recordset.md) メソッドをサポートします。|  
|**adFind**|0x80000|では、[レコードセット](./recordset-object-ado.md)内の行を検索するための[Find](./find-method-ado.md)メソッドがサポートされています。|  
|**adHoldRecords**|0x100|すべての保留中の変更をコミットせずに、より多くのレコードを取得するか、次の位置を変更します。|  
|**adIndex**|0x100000|インデックスの名前を指定する [index](./index-property.md) プロパティをサポートしています。|  
|**adMovePrevious**|0x200|は、 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) および [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) メソッドをサポートします。また、ブックマークを必要とせずに現在のレコードの位置を後方に移動するには、 [move](./move-method-ado.md) メソッドまたは [GetRows](./getrows-method-ado.md) メソッドを使用します。|  
|**adNotify**|0x40000|基になるデータプロバイダーが通知をサポートしていることを示します。これは、 **レコードセット** イベントがサポートされるかどうかを決定します。|  
|**adResync**|0x20000|は、基になるデータベースで表示されているデータを使用してカーソルを更新するための再 [同期](./resync-method.md) メソッドをサポートしています。|  
|**adSeek**|0x200000|では、**レコードセット**内の行を検索する[Seek](./seek-method.md)メソッドがサポートされています。|  
|**adUpdate**|0x1008000|では、既存のデータを変更するための [Update](./update-method.md) メソッドがサポートされています。|  
|**adUpdateBatch**|0x10000|では、バッチ更新 ([UpdateBatch](./updatebatch-method.md) および [CancelBatch](./cancelbatch-method-ado.md) メソッド) をサポートして、変更のグループをプロバイダーに送信します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums を指定します。|  
|AdoEnums. APPROXPOSITION|  
|AdoEnums を指定します。|  
|AdoEnums を削除します。|  
|AdoEnums を参照してください。|  
|AdoEnums HOLDRECORDS|  
|AdoEnums を指定します。|  
|AdoEnums MOVEPREVIOUS|  
|AdoEnums を指定します。通知|  
|AdoEnums の再同期|  
|AdoEnums を検索します。|  
|AdoEnums を更新します。|  
|AdoEnums. UPDATEBATCH|  
  
## <a name="applies-to"></a>適用対象  
 [Supports メソッド](./supports-method.md)