---
description: ADCPROP_ASYNCTHREADPRIORITY_ENUM
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: rothja
ms.author: jroth
ms.openlocfilehash: ff25342a8ba7976b883ecdca8e55f8695bf45099
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100031474"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
RDS [レコードセット](./recordset-object-ado.md) オブジェクトの場合は、データを取得する非同期スレッドの実行の優先度を指定します。  
  
 これらの定数は、 **レコードセット** の "**バックグラウンドスレッド優先順位**" 動的プロパティと共に使用します。これは、ADO から OLE DB の動的プロパティインデックスで参照され、 [OLE DB のドキュメントについては Microsoft Cursor Service](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) に記載されています。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|通常と最高の間の優先順位を設定します。|  
|**adPriorityBelowNormal**|2|最低と通常の優先順位を設定します。|  
|**Adの優先順位**|5|優先順位を可能な限り高く設定します。|  
|**Adの優先順位の下限**|1|優先順位を可能な限り低く設定します。|  
|**Ad優先度標準**|3|優先順位を normal に設定します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums を ABOVENORMAL します。|  
|AdoEnums を BELOWNORMAL します。|  
|AdoEnums を最大にします。|  
|AdoEnums を最小にします。|  
|AdoEnums。通常の場合は、|