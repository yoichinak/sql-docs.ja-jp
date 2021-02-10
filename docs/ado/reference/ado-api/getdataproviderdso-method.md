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
ms.openlocfilehash: 6994b3c5466622a32ad0d17e1a00424396d39ebc
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100021224"
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
  
## <a name="remarks"></a>解説  
 このメソッドは、インターフェイスポインターを addref しません。 呼び出し元がポインターを保持することを計画している場合、呼び出し元は必要な addref と release を実行する必要があります。  
  
## <a name="applies-to"></a>適用対象  
 [IDSOShapeExtensions インターフェイス](./idsoshapeextensions-interface.md)