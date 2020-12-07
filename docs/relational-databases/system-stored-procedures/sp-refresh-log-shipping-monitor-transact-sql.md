---
description: sp_refresh_log_shipping_monitor (Transact-SQL)
title: sp_refresh_log_shipping_monitor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3ece1b616c1639a7e826f6c5d5cc566ec8cb35b6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549567"
---
# <a name="sp_refresh_log_shipping_monitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  リモートの監視テーブルを、指定したログ配布エージェントの特定のプライマリまたはセカンダリ サーバーにある最新の情報に更新します。 プロシージャは、プライマリサーバーまたはセカンダリサーバーで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>引数  
`[ @agent_id = ] 'agent_id'` バックアップ用のプライマリ ID、またはコピーまたは復元用のセカンダリ ID。 *agent_id* は **uniqueidentifier** であり、NULL にすることはできません。  
  
`[ @agent_type = ] 'agent_type'` ログ配布ジョブの種類です。  
  
 0 = バックアップ。  
  
 1 = コピー。  
  
 2 = 復元します。  
  
 *agent_type* は **tinyint** であり、NULL にすることはできません。  
  
`[ @database = ] 'database'` バックアップまたは復元エージェントによってログに記録されるプライマリデータベースまたはセカンダリデータベース。  
  
`[ @mode ] n` モニターデータを更新するか、クリーンアップするかを指定します。 *M*のデータ型は tinyint であり、サポートされている値は次のとおりです。  
  
 1 = 更新 (既定値)  
  
 2 = delete  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [なし] :  
  
## <a name="remarks"></a>解説  
 **sp_refresh_log_shipping_monitor** は、まだ転送されていないセッション情報を使用して、 **log_shipping_monitor_primary**、 **log_shipping_monitor_secondary**、 **log_shipping_monitor_history_detail**、および **log_shipping_monitor_error_detail** のテーブルを更新します。 これにより、モニターがしばらく同期されていない場合に、監視サーバーをプライマリサーバーまたはセカンダリサーバーと同期することができます。 また、必要に応じて、監視サーバーのモニター情報をクリーンアップすることができます。  
  
 **sp_refresh_log_shipping_monitor** は、プライマリサーバーまたはセカンダリサーバーの **master** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
