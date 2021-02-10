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
ms.openlocfilehash: f287d19a4a34e9c71f06aab63910465ade3982d2
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100024196"
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