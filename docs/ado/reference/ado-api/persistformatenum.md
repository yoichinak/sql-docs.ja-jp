---
description: PersistFormatEnum
title: PersistFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
author: rothja
ms.author: jroth
ms.openlocfilehash: 25214603d009cfa8203aabe482ffdd7b511dd169
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170573"
---
# <a name="persistformatenum"></a>PersistFormatEnum
[レコードセット](./recordset-object-ado.md)を保存する形式を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Microsoft Advanced Data TableGram (ADTG) 形式を示します。|  
|**adPersistADO**|1|ADO の独自の拡張マークアップ言語 (XML) 形式が使用されることを示します。 この値は adPersistXML と同じであり、旧バージョンとの互換性のために用意されています。|  
|**adPersistXML**|1|拡張マークアップ言語 (XML) 形式を示します。|  
|**adPersistProviderSpecific**|2|プロバイダーが独自の形式を使用して **レコードセット** を永続化することを示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>適用対象  
 [Save メソッド](./save-method.md)