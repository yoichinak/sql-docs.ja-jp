---
description: ADCPROP_UPDATERESYNC_ENUM
title: ADCPROP_UPDATERESYNC_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
author: rothja
ms.author: jroth
ms.openlocfilehash: ca1583203ced1f1ce8ed54f7624d21d7b4cfa482
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99161746"
---
# <a name="adcprop_updateresync_enum"></a>ADCPROP_UPDATERESYNC_ENUM
[UpdateBatch](./updatebatch-method.md)メソッドの後に暗黙の再[同期](./resync-method.md)メソッド操作が続くかどうかを指定します。それを行う場合は、その操作のスコープを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|他のすべての ADCPROP_UPDATERESYNC_ENUM メンバーの結合された値を使用して再 **同期** を呼び出します。|  
|**adResyncAutoIncrement**|1|既定値。 データソースによって自動的にインクリメントまたは生成される列の新しい id 値の取得を試みます。これには、Microsoft Jet のオートナンバーフィールドや Microsoft SQL Server Id 列などがあります。|  
|**adResyncConflicts**|2|同時実行の競合により、更新または削除操作が失敗したすべての行に対して再 **同期** を呼び出します。|  
|**adResyncInserts**|8|正常に挿入されたすべての行の再 **同期** を呼び出します。 ただし、AutoIncrement 列の値は再同期されません。 代わりに、新しく挿入された行の内容が、既存の主キーの値に基づいて再同期されます。 主キーが AutoIncrement 値の場合、再 **同期** は目的の行の内容を取得しません。 自動インクリメントの主キー値を自動的にインクリメントする場合は、 **adResyncAutoIncrement** adResyncInserts の値を組み合わせて **UpdateBatch** を呼び出し  +  ます。|  
|**adResyncNone**|0|再 **同期** を呼び出しません。|  
|**adResyncUpdates**|4|正常に更新されたすべての行に対して再 **同期** を呼び出します。|  
  
## <a name="applies-to"></a>適用対象  
 [Update Resync プロパティ - 動的 (ADO)](./update-resync-property-dynamic-ado.md)