---
description: Chapter プロパティ (ADO)
title: Chapter プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: rothja
ms.author: jroth
ms.openlocfilehash: ea7810e7b829991d185edf49f8224db57535f947
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975523"
---
# <a name="chapter-property-ado"></a>Chapter プロパティ (ADO)
[ADORecordsetConstruction Interface](./adorecordsetconstruction-interface.md)オブジェクトから OLE DB**チャプター**オブジェクトを取得します。値の設定もできます。 **Put_Chapter**を使用して**チャプター**オブジェクトを設定すると、行のサブセットが ADO[レコードセットオブジェクト](./recordset-object-ado.md)オブジェクトに変換されます。 これにより、 **行セット**オブジェクトの現在のチャプターが設定されます。 このプロパティは読み取り/書き込み可能です。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>パラメーター  
 *plChapter*  
 チャプターのハンドルへのポインター。  
  
 *LChapter*  
 チャプターのハンドル。  
  
## <a name="return-values"></a>戻り値  
 このプロパティメソッドは、S_OK および E_FAIL を含む標準の HRESULT 値を返します。  
  
## <a name="applies-to"></a>適用対象  
 [ADORecordsetConstruction インターフェイス](./adorecordsetconstruction-interface.md)