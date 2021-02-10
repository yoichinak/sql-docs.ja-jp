---
description: IDSOShapeExtensions インターフェイス
title: Idsoの拡張機能の Interface |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
author: rothja
ms.author: jroth
ms.openlocfilehash: 329c7b3193bd86ad05c757229477b5934d6e650d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100020799"
---
# <a name="idsoshapeextensions-interface"></a>IDSOShapeExtensions インターフェイス
図形プロバイダーの基になる OLE DB データソースオブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
interface IDSOShapeExtensions: public IUnknown {  
public:  
      HRESULT  GetDataProviderDSO(  
            IUnknown **ppDataProviderDSOIUnknown  
      );  
};  
```  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|-|-|  
|[GetDataProviderDSO メソッド](./getdataproviderdso-method.md)|基になる OLE DB データソースオブジェクトをシェイププロバイダーから取得します。|  
  
## <a name="requirements"></a>必要条件  
 **バージョン:** ADO 2.0 以降  
  
 **ライブラリ:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4