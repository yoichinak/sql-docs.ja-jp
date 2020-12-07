---
title: KILL QUERY NOTIFICATION SUBSCRIPTION
description: インスタンスからクエリ通知サブスクリプションを削除します。 このステートメントでは、特定のサブスクリプションまたはすべてのサブスクリプションを削除できます。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION
- KILL_QUERY_NOTIFICATION_SUBSCRIPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION statement
- removing subscriptions
- subscriptions [SQL Server query notifications], stopping
- query notifications [SQL Server], subscriptions
ms.assetid: 8aeadf51-286c-4748-bef2-d25858b250bf
author: rothja
ms.author: jroth
ms.openlocfilehash: 0434642595fb334c138e1c3d1764384760a38407
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193372"
---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  インスタンスからクエリ通知サブスクリプションを削除します。 このステートメントでは、特定のサブスクリプションまたはすべてのサブスクリプションを削除できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 ALL  
 インスタンス内のすべてのサブスクリプションを削除します。  
  
 *subscription_id*  
 *subscription_id* で指定したサブスクリプション ID のサブスクリプションを削除します。  
  
## <a name="remarks"></a>解説  
 KILL QUERY NOTIFICATION SUBSCRIPTION ステートメントでクエリ通知サブスクリプションを削除する際、通知メッセージは生成されません。  
  
 *subscription_id* には、動的管理ビュー [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md) に表示されるサブスクリプションの ID を指定します。  
  
 指定したサブスクリプション ID が存在しない場合は、エラーが発生します。  
  
## <a name="permissions"></a>アクセス許可  
 このステートメントの実行権限は、**sysadmin** 固定サーバー ロールのメンバーに制限されます。  
  
## <a name="examples"></a>例  
  
### <a name="a-removing-all-query-notification-subscriptions-in-the-instance"></a>A. インスタンス内のすべてのクエリ通知サブスクリプションを削除する  
 次の例では、インスタンス内のすべてのクエリ通知サブスクリプションを削除します。  
  
```sql  
KILL QUERY NOTIFICATION SUBSCRIPTION ALL ;  
```  
  
### <a name="b-removing-a-single-query-notification-subscription"></a>B. 1 つのクエリ通知サブスクリプションを削除する  
 次の例では、サブスクリプション ID が `73` のクエリ通知サブスクリプションを削除します。  
  
```sql  
KILL QUERY NOTIFICATION SUBSCRIPTION 73 ;  
```  
  
## <a name="see-also"></a>参照  
 [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  
