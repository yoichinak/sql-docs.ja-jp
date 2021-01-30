---
description: managed_backup managed_backup.fn_get_parameter (transact-sql)
title: managed_backup managed_backup.fn_get_parameter (transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- smart_admin.fn_get_parameter_TSQL
- smart_admin.fn_get_parameter
- fn_get_parameter_TSQL
- fn_get_parameter
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_parameter
- smart_admin.fn_get_parameter
ms.assetid: ed94e54d-4516-4806-a8ce-f013d3a04122
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a30e80c084768df7a40977c052a8649adeae33fc
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99207390"
---
# <a name="managed_backupfn_get_parameter-transact-sql"></a>managed_backup managed_backup.fn_get_parameter (transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  パラメーターと値のペアから成る 0 行、1 行、または複数行を格納したテーブルを返します。  
  
 このストアド プロシージャを使用すると、Smart Admin のすべてまたは特定の構成設定を確認できます。  
  
 パラメーターがまだ構成されていない場合は、この関数は 0 行を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
managed_backup.fn_get_parameter ('parameter_name' | '' | NULL )  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 parameter_name  
 パラメーターの名前。 parameter_name は **NVARCHAR (128)** です。 関数に NULL または空の文字列が引数として指定されている場合は、構成されているすべてのスマート管理パラメーターの名前と値のペアが返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|parameter_name|NVARCHAR (128)|パラメーターの名前。 返されるパラメーターの現在の一覧を次に示します。<br/><br/>**FileRetentionDebugXevent**<br/><br/>**SSMBackup2WADebugXevent**<br/><br/>**SSMBackup2WANotificationEmailIds**<br/><br/>**SSMBackup2WAEnableUserDefinedPolicy**<br/><br/>**SSMBackup2WAEverConfigured**<br/><br/>**StorageOperationDebugXevent**|  
|parameter_value|NVARCHAR (128)|パラメーターの現在設定されている値。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 この関数に対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、少なくとも1回構成されているすべてのパラメーターと、それらの現在の値を返します。  
  
```  
USE MSDB  
GO  
SELECT *   
FROM managed_backup.fn_get_parameter (NULL)  
  
```  
  
 次の例では、エラー通知の受信先として指定された電子メール ID を返します。 返される行がない場合は、この電子メール通知オプションが有効になっていないことを意味します。  
  
```  
USE MSDB  
GO  
SELECT *  
FROM managed_backup.fn_get_parameter ('SSMBackup2WANotficationEmailIds')  
  
```  
  
## <a name="see-also"></a>参照  
 [Microsoft Azure への SQL Server マネージド バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
