---
description: put_OLEDBCommand メソッド
title: put_OLEDBCommand メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
helpviewer_keywords:
- put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
author: rothja
ms.author: jroth
ms.openlocfilehash: c124bfa83dc9c8546d968b7292850086fa393a25
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166780"
---
# <a name="put_oledbcommand-method"></a>put_OLEDBCommand メソッド
このメソッドは操作を実行せず、常に S_OK を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pOLEDBCommand*  
 からOLE DB Command オブジェクトへのポインター。  
  
## <a name="applies-to"></a>適用対象  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))