---
description: GetDataProviderDSO メソッド
title: GetDataProviderDSO メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: rothja
ms.author: jroth
ms.openlocfilehash: c784e5c3951f78ef28bfd0d0008570d1b1e68ca8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167277"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO メソッド
基になる OLE DB データソースオブジェクトをシェイププロバイダーから取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ppDataProviderDSOIUnknown*  
 入出力 基になる OLE DB データソースオブジェクトの IUnknown を返すポインターへのポインター。  
  
## <a name="remarks"></a>コメント  
 このメソッドは、インターフェイスポインターを addref しません。 呼び出し元がポインターを保持することを計画している場合、呼び出し元は必要な addref と release を実行する必要があります。  
  
## <a name="applies-to"></a>適用対象  
 [IDSOShapeExtensions インターフェイス](./idsoshapeextensions-interface.md)