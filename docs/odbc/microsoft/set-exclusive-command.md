---
description: SET EXCLUSIVE コマンド
title: SET EXCLUSIVE Command |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43cd58e5e9f714de0defe36cea020ccb96ac3efa
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99208631"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE コマンド
ネットワーク上でテーブルファイルを排他的に使用するか共有するかを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 ネットワーク上で開かれているテーブルのアクセシビリティを、そのネットワークを開いたユーザーに制限します。 このテーブルには、ネットワーク上の他のユーザーがアクセスできません。 [排他モードに設定すると、他のすべてのユーザーに読み取り専用アクセスを許可しないようにすることもできます。  
  
 OFF  
 (ドライバーの既定値は、グローバルデータセッションでは Visual FoxPro、プライベートデータセッションでは OFF です)。ネットワーク上で開いているテーブルをネットワーク上の任意のユーザーが共有および変更できるようにします。  
  
## <a name="remarks"></a>コメント  
 SET EXCLUSIVE の設定を変更しても、以前に開いたテーブルの状態は変更されません。 たとえば、SET EXCLUSIVE が ON に設定された状態でテーブルを開き、SET EXCLUSIVE を後で OFF に変更した場合、テーブルはその排他使用状態を保持します。  
  
## <a name="see-also"></a>参照  
 [ODBC Visual FoxPro セットアップ ダイアログ ボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
