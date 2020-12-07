---
description: SET UNIQUE コマンド
title: UNIQUE コマンドの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8fa4ca11ed5beae08bfcbeb8b5a55d6c2969785
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412458"
---
# <a name="set-unique-command"></a>SET UNIQUE コマンド
重複するインデックスキー値を持つレコードをインデックスファイルで保持するかどうかを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 重複するインデックスキー値を持つすべてのレコードをインデックスファイルに含めないように指定します。 インデックスファイルには、元のインデックスキー値を持つ最初のレコードだけが含まれます。  
  
 OFF  
 (既定値)。重複するインデックスキー値を持つレコードをインデックスファイルに含めることを指定します。  
  
## <a name="remarks"></a>解説  
 インデックスファイルは、REINDEX を発行するときに、設定された一意の設定を保持します。 詳細については、「 [INDEX](../../odbc/microsoft/index-command.md)」を参照してください。
