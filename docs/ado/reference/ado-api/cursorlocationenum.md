---
description: CursorLocationEnum
title: カーソル Locationenum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: rothja
ms.author: jroth
ms.openlocfilehash: e6e504948e2aaf76c52d424945f76373bb38697a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100034542"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
カーソルサービスの場所を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|では、ローカルカーソルライブラリによって提供されるクライアント側カーソルが使用されます。 多くの場合、ローカルカーソルサービスでは、ドライバーによって提供されるカーソルが使用できない多くの機能を使用できます。そのため、この設定を使用すると、有効になる機能に対して利点が得られる可能性があります。 旧バージョンとの互換性のために、シノニム **adUseClientBatch** もサポートされています。|  
|**adUseNone**|1|カーソルサービスを使用しません。 (この定数は互換性のために残されており、旧バージョンとの互換性のためだけに残されています)。|  
|**adUseServer**|2|既定値。 データプロバイダーまたはドライバーによって提供されるカーソルを使用します。 これらのカーソルは、非常に柔軟性が高く、他のユーザーがデータソースに対して行う変更に対して、さらに機密性を高めることができます。 ただし、 [OLE DB 用の Microsoft Cursor Service](../../guide/data/the-microsoft-cursor-service-for-ole-db.md)の一部の機能 (関連付けの解除など)<br /><br /> [レコードセット](./recordset-object-ado.md) オブジェクトは、サーバー側カーソルではシミュレートできません。これらの機能は、この設定では使用できません。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums を指定します。|  
|AdoEnums. NONE|  
|AdoEnums. サーバー|  
  
## <a name="applies-to"></a>適用対象  
 [CursorLocation プロパティ (ADO)](./cursorlocation-property-ado.md)