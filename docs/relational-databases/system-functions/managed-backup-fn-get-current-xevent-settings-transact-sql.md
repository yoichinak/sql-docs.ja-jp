---
description: managed_backup。 fn_get_current_xevent_settings (Transact-sql)
title: managed_backup。 fn_get_current_xevent_settings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_current_xevent_settings
- smart_admin.fn_get_current_xevent_settings_TSQL
- fn_get_current_xevent_settings_TSQL
- smart_admin.fn_get_current_xevent_settings
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_current_xevent_settings
- fn_get_current_xevent_settings
ms.assetid: 95d3adaa-bb9d-4833-b8b4-3d9fd4f9c82a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 164038c2009f273ae922e65c922c1d962a72b7d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419526"
---
# <a name="managed_backupfn_get_current_xevent_settings-transact-sql"></a>managed_backup。 fn_get_current_xevent_settings (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  スマートな制御者によってサポートされる拡張イベントの種類ごとに1行の値を返します。  
  
 この関数を使用すると、現在の拡張イベントの設定を返したり、確認したりして、構成可能なイベントの種類と現在の構成を識別できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
smart_admin.fn_get_current_xevent_settings ()   
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 この関数には引数がありません。  
  
## <a name="table-returned"></a>返されるテーブル  
 拡張イベントの管理、分析、運用のチャネルは必須であり、既定で有効になっていますが、構成することはできません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|Event_name|NVARCHAR (128)|拡張イベントの種類|  
|is_configurable|NVARCHAR (128)|イベントが構成可能な場合は **True** に設定され、それ以外の場合は **False**に設定されます。|  
|is_enabled|NVARCHAR (128)|イベントが有効な場合は True に設定されます。有効でない場合は False に設定されます。 デバッグ イベントを有効にするには、smart_admin.sp_set_parameter を使用します。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 関数に対する **SELECT** 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、すべての拡張イベントが現在の状態と共に返されます。  
  
```  
SELECT *   
FROM smart_admin.fn_get_current_xevent_settings ()  
  
```  
  
  
