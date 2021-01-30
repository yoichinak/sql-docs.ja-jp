---
description: Rowset プロパティ (ADO)
title: Rowset プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords:
- Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
author: rothja
ms.author: jroth
ms.openlocfilehash: 1f5e99f97179323e92ff04153b5cb9fe0d67fe46
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170336"
---
# <a name="rowset-property-ado"></a>Rowset プロパティ (ADO)
**ADORecordsetConstruction** オブジェクトの/から OLE DB **行セット** オブジェクトを取得します。値の設定もできます。 Put_Rowset を使用すると、行セットは ADO **レコードセット** オブジェクトに変換されます。  
  
 読み取りと書き込みが可能です。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>パラメーター  
 *ppRowset*  
 OLE DB **行セット** オブジェクトへのポインター。  
  
 *PRowset*  
 OLE DB **行セット** オブジェクト。  
  
## <a name="return-values"></a>戻り値  
 このプロパティメソッドは、S_OK および E_FAIL を含む標準の HRESULT 値を返します。  
  
## <a name="applies-to"></a>適用対象  
 [ADORecordsetConstruction インターフェイス](./adorecordsetconstruction-interface.md)