---
description: IsolationLevelEnum
title: IsolationLevelEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
author: rothja
ms.author: jroth
ms.openlocfilehash: d56051369218f8700ef516526c3f1baf07c7469b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990763"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
[接続](./connection-object-ado.md)オブジェクトのトランザクション分離レベルを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|プロバイダーが指定とは異なる分離レベルを使用しているが、レベルを特定できないことを示します。|  
|**adXactChaos**|16|より高度な分離トランザクションからの保留中の変更を上書きできないことを示します。|  
|**adXactBrowse**|256|あるトランザクションから、コミットされていない変更を他のトランザクションで表示できることを示します。|  
|**が adxactreaduncommitted**|256|**AdXactBrowse**と同じです。|  
|**adXactCursorStability**|4096|は、トランザクションがコミットされた後にのみ、他のトランザクションの変更を表示できることを示します。|  
|**adXactReadCommitted**|4096|**AdXactCursorStability**と同じです。|  
|**adXactRepeatableRead**|65536|1つのトランザクションから、他のトランザクションで行われた変更を表示できないが、再実行によって新しい **レコードセット** オブジェクトを取得できることを示します。|  
|**adXactIsolated**|1048576|トランザクションが他のトランザクションとは別に実行されることを示します。|  
|**adXactSerializable**|1048576|**AdXactIsolated**と同じです。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums. IsolationLevel|  
|AdoEnums IsolationLevel|  
|AdoEnums IsolationLevel|  
|AdoEnums. IsolationLevel. READUNCOMMITTED|  
|AdoEnums IsolationLevel|  
|AdoEnums IsolationLevel|  
|AdoEnums. IsolationLevel. REPEATABLEREAD|  
|AdoEnums IsolationLevel|  
|AdoEnums IsolationLevel|  
  
## <a name="applies-to"></a>適用対象  
 [IsolationLevel プロパティ](./isolationlevel-property.md)