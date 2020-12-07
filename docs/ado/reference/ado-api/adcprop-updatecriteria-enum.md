---
description: ADCPROP_UPDATECRITERIA_ENUM
title: ADCPROP_UPDATECRITERIA_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: rothja
ms.author: jroth
ms.openlocfilehash: 3711266f3658fe2366caa56c6afba07d6b63c4c9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976813"
---
# <a name="adcprop_updatecriteria_enum"></a>ADCPROP_UPDATECRITERIA_ENUM
[レコードセット](./recordset-object-ado.md)オブジェクトを使用してデータソースの行をオプティミスティック更新するときに、競合を検出するために使用できるフィールドを指定します。  
  
 これらの定数を **レコードセット** "**Update Criteria**" と共に使用します。動的プロパティは [ADO 動的プロパティインデックス](./ado-dynamic-property-index.md) で参照され、 [OLE DB のドキュメントについては Microsoft Cursor Service](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) に記載されています。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**Ad? Aallcols**|1|データソース行の列が変更された場合に、競合を検出します。|  
|**Ad? Akey**|0|では、データソース行のキー列が変更された場合に競合が検出されます。これは、その行が削除されたことを意味します。|  
|**Adme・スタンプ**|3|では、データソース行のタイムスタンプが変更された場合に競合を検出します。これは、 **レコードセット** が取得された後に行にアクセスしたことを意味します。|  
|**Adの場合**|2|**レコードセット**の更新されたフィールドに対応するデータソース行の列のいずれかが変更された場合に、競合を検出します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums AdcPropUpdateCriteria|  
|AdoEnums AdcPropUpdateCriteria|  
|AdoEnums AdcPropUpdateCriteria|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|