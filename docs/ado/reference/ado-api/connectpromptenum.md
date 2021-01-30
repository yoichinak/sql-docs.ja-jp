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
ms.openlocfilehash: 7563179d70968cc98fbbc1055ec32c2c3a1948f0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167698"
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