---
description: SET UNIQUE コマンド
title: UNIQUE コマンドの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f30e589349ab1f0388e43af0aec132465b1fcdce
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99208584"
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
  
## <a name="remarks"></a>コメント  
 インデックスファイルは、REINDEX を発行するときに、設定された一意の設定を保持します。 詳細については、「 [INDEX](../../odbc/microsoft/index-command.md)」を参照してください。
