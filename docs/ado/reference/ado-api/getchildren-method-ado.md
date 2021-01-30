---
description: GetChildren メソッド (ADO)
title: GetChildren メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: rothja
ms.author: jroth
ms.openlocfilehash: cb49de0d3613cca9d24991e67ee8787c0d863b8c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167285"
---
# <a name="getchildren-method-ado"></a>GetChildren メソッド (ADO)
コレクション[レコード](./record-object-ado.md)の子を表す行を含む[レコードセット](./recordset-object-ado.md)を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>戻り値  
 各行が現在の **レコード** オブジェクトの子を表す **Recordset** オブジェクト。 たとえば、ディレクトリを表す **レコード** の子は、親ディレクトリに格納されているファイルおよびサブディレクトリになります。  
  
## <a name="remarks"></a>コメント  
 プロバイダーは、返された **レコードセット** に存在する列を決定します。 たとえば、ドキュメントソースプロバイダーは常にリソース **レコードセット** を返します。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Record オブジェクト (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::