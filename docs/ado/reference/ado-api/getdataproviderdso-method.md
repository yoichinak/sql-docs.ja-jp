---
description: GetDataProviderDSO メソッド
title: GetDataProviderDSO メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: rothja
ms.author: jroth
ms.openlocfilehash: 85e701cb7ce725aa9afa9d682467c1a97f5dd378
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972903"
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