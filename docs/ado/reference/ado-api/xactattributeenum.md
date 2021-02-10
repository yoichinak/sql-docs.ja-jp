---
description: XactAttributeEnum
title: XactAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: rothja
ms.author: jroth
ms.openlocfilehash: e741ec0e5458218ddb6dc3a46c3a098acf482611
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100056027"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
[接続](./connection-object-ado.md)オブジェクトのトランザクション属性を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|[RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)を呼び出して新しいトランザクションを自動的に開始することによって、中断を保持します。 すべてのプロバイダーがこの動作をサポートするわけではありません。|  
|**adXactCommitRetaining**|131072|[CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)を呼び出して、新しいトランザクションを自動的に開始することによって、コミットの保持を実行します。 すべてのプロバイダーがこの動作をサポートするわけではありません。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>適用対象  
 [Attributes プロパティ (ADO)](./attributes-property-ado.md)