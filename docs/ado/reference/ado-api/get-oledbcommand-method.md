---
description: get_OLEDBCommand メソッド
title: get_OLEDBCommand メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
author: rothja
ms.author: jroth
ms.openlocfilehash: edd8816389088c077f43ed7b36f01ebd61010e98
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99171007"
---
# <a name="get_oledbcommand-method"></a>get_OLEDBCommand メソッド
基になる OLE DB コマンドを返します。最初に ADO コマンドで設定されたすべてのパラメーター情報を OLE DB コマンドに反映します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ppOLEDBCommand*  
 入出力基になる OLE DB コマンドの IUnknown ポインターが書き込まれるポインター位置へのポインター。  
  
## <a name="applies-to"></a>適用対象  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))