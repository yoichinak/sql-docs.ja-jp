---
description: SeekEnum
title: SeekEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: rothja
ms.author: jroth
ms.openlocfilehash: 3286e6d6477cf18f95d95ccd494336e7a119f009
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100051453"
---
# <a name="seekenum"></a>SeekEnum
実行する [シーク](./seek-method.md) の種類を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**Adseekの Steq**|1|*Keyvalues* と等しい最初のキーをシークします。|  
|**adSeekLastEQ**|2|*Keyvalues* と等しい最後のキーをシークします。|  
|**adSeekAfterEQ**|4|*Keyvalues* と等しいキー、またはその直後に一致したキーをシークします。|  
|**adSeekAfter**|8|*Keyvalues* との一致が発生した直後にキーをシークします。|  
|**adSeekBeforeEQ**|16|*Keyvalues* と等しいキー、またはその一致が発生した直前のキーをシークします。|  
|**adSeekBefore**|32|*Keyvalues* との一致が発生する直前に、キーをシークします。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums を検索します。|  
|AdoEnums を検索します。|  
|AdoEnums. AFTEREQ|  
|AdoEnums|  
|AdoEnums。|  
|AdoEnums|  
  
## <a name="applies-to"></a>適用対象  
 [Seek メソッド](./seek-method.md)