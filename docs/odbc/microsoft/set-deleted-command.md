---
description: SET DELETED コマンド
title: SET DELETED コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60e00af582e0440957c8a4e743624e00f0ba3e58
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466374"
---
# <a name="set-deleted-command"></a>SET DELETED コマンド
削除用にマークされたレコードを処理するかどうか、および他のコマンドで使用できるかどうかを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 (ドライバーの既定値は、Visual FoxPro の既定値は OFF です)。スコープを使用してレコード (関連テーブル内のレコードを含む) を操作するコマンドが、削除対象としてマークされたレコードを無視するように指定します。  
  
 OFF  
 スコープを使用してレコード (関連テーブル内のレコードを含む) を操作するコマンドから、削除対象としてマークされたレコードにアクセスできることを指定します。  
  
## <a name="remarks"></a>解説  
 Deleted () を使用してレコードの状態をテストするクエリは、削除された () に対してテーブルのインデックスが作成されている場合、Visual FoxPro Rushmore テクノロジを使用して最適化できます。  
  
> [!IMPORTANT]  
>  コマンドの既定のスコープが現在のレコードである場合、または1つのレコードのスコープを含める場合は、SET DELETED は無視されます。 インデックスは常に、SET DELETED を無視し、テーブル内のすべてのレコードにインデックスを設定します。  
  
## <a name="see-also"></a>関連項目  
 [DELETE - SQL コマンド](../../odbc/microsoft/delete-sql-command.md)
