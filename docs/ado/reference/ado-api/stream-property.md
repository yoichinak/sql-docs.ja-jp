---
description: Stream プロパティ
title: Stream プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
author: rothja
ms.author: jroth
ms.openlocfilehash: b65a3bf2d4664be84250a9923f0ed3908c07f179
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170135"
---
# <a name="stream-property"></a>Stream プロパティ
**ADOStreamConstruction** オブジェクトからの OLE DB **ストリーム** オブジェクトを取得します。値の設定もできます。  
  
 読み取りと書き込みが可能です。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>パラメーター  
 *ppStream*  
 OLE DB **ストリーム** オブジェクトへのポインター。  
  
 *pStream*  
 OLE DB **ストリーム** オブジェクト。  
  
## <a name="return-values"></a>戻り値  
 このプロパティメソッドは、標準の HRESULT 値を返します。 これには、S_OK と E_FAIL が含まれます。  
  
## <a name="applies-to"></a>適用対象  
 [ADOStreamConstruction インターフェイス](./adostreamconstruction-interface.md)