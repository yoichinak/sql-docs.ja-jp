---
description: ConnectPromptEnum
title: ConnectPromptEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: rothja
ms.author: jroth
ms.openlocfilehash: 98a4e0d65ffb0596825557813cf12266b9fe79ed
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100034622"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
データソースへの接続を開くときにダイアログボックスを表示して、不足しているパラメーターを確認するかどうかを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|常にプロンプトを表示します。|  
|**adPromptComplete**|2|詳細情報が必要かどうかを確認するメッセージが表示されます。|  
|**adPromptCompleteRequired**|3|詳細情報が必要かどうかを確認するメッセージが表示されますが、省略可能なパラメーターは使用できません。|  
|**adPromptNever**|4|プロンプトが表示されません。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums を常に確認します。|  
|AdoEnums を実行します。|  
|AdoEnums COMPLETEREQUIRED|  
|AdoEnums。 NEVER|  
  
## <a name="applies-to"></a>適用対象  
 [Prompt プロパティ - 動的 (ADO)](./prompt-property-dynamic-ado.md)