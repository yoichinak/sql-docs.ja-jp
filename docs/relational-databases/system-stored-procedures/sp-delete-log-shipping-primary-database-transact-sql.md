---
description: sp_delete_log_shipping_primary_database (Transact-SQL)
title: sp_delete_log_shipping_primary_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2b7a1e58188a9b9f3a845e465139e5a24d3fad88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474389"
---
# <a name="sp_delete_log_shipping_primary_database-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  バックアップ ジョブ、ローカル履歴、およびリモート履歴を含むプライマリ データベースのログ配布を削除します。 **Sp_delete_log_shipping_primary_secondary**を使用してセカンダリデータベースを削除した後にのみ、このストアドプロシージャを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>引数  
`[ @database = ] 'database'` ログ配布プライマリデータベースの名前を指定します。 *データベースのデータ* 型は **sysname**で、既定値はありません。 NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [なし] :  
  
## <a name="remarks"></a>解説  
 **sp_delete_log_shipping_primary_database** は、プライマリサーバーの **master** データベースから実行する必要があります。 このストアド プロシージャでは次の処理が行われます。  
  
1.  指定されたプライマリデータベースのバックアップジョブを削除します。  
  
2.  プライマリサーバー上の **log_shipping_monitor_primary** のローカル監視レコードを削除します。  
  
3.  **Log_shipping_monitor_history_detail**と**log_shipping_monitor_error_detail**内の対応するエントリを削除します。  
  
4.  監視サーバーがプライマリサーバーと異なる場合は、監視サーバーの **log_shipping_monitor_primary** の監視レコードを削除します。  
  
5.  監視サーバー上の **log_shipping_monitor_history_detail** と **log_shipping_monitor_error_detail** 内の対応するエントリを削除します。  
  
6.  このプライマリデータベースの **log_shipping_primary_databases** のエントリを削除します。  
  
7.  監視サーバーで **sp_delete_log_shipping_alert_job** を呼び出します。  

## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 この例では、 **sp_delete_log_shipping_primary_database** を使用して、プライマリデータベース **AdventureWorks2012**を削除しています。  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
