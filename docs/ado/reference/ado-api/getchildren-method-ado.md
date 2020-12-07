---
description: GetChildren メソッド (ADO)
title: GetChildren メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: rothja
ms.author: jroth
ms.openlocfilehash: ea59a94f095a438be8fc7009a58179d488af20a2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972833"
---
# <a name="getchildren-method-ado"></a>GetChildren メソッド (ADO)
コレクション[レコード](./record-object-ado.md)の子を表す行を含む[レコードセット](./recordset-object-ado.md)を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>戻り値  
 各行が現在の**レコード**オブジェクトの子を表す**Recordset**オブジェクト。 たとえば、ディレクトリを表す **レコード** の子は、親ディレクトリに格納されているファイルおよびサブディレクトリになります。  
  
## <a name="remarks"></a>解説  
 プロバイダーは、返された **レコードセット**に存在する列を決定します。 たとえば、ドキュメントソースプロバイダーは常にリソース **レコードセット**を返します。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Record オブジェクト (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::