---
description: ALTER SERVICE (Transact-SQL)
title: ALTER SERVICE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SERVICE
- ALTER_SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying services
- contracts [Service Broker], modifying
- ALTER SERVICE statement
- services [Service Broker], modifying
ms.assetid: 2b4608f7-bb2e-4246-aa29-b52c55995b3a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c6a9ed30e92358d269fa4d6c0e270bd4a16e3bdb
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126252"
---
# <a name="alter-service-transact-sql"></a>ALTER SERVICE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  既存のサービスを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql 
ALTER SERVICE service_name   
   [ ON QUEUE [ schema_name . ]queue_name ]   
   [ ( < opt_arg > [ , ...n ] ) ]  
[ ; ]  
  
<opt_arg> ::=  
   ADD CONTRACT contract_name | DROP CONTRACT contract_name  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *service_name*  
 変更するサービス名を指定します。 サーバー名、データベース名、スキーマ名は指定できません。  
  
 ON QUEUE [ _schema_name_**.** ] *queue_name*  
 このサービス用の新しいキューを指定します。 このサービス用のすべてのメッセージは、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によって現在のキューから新しいキューに移動されます。  
  
 ADD CONTRACT *contract_name*  
 このサービスで公開されるコントラクト セットに追加するコントラクトを指定します。  
  
 DROP CONTRACT *contract_name*  
 このサービスで公開されるコントラクト セットから削除するコントラクトを指定します。 このコントラクトを使用するサービスとのメッセージ交換が存在する場合、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によってエラー メッセージが送信されます。  
  
## <a name="remarks"></a>注釈  
 ALTER SERVICE ステートメントによってサービスからコントラクトが削除されると、サービスは、このコントラクトを使用するメッセージ交換の対象から除外されます。 したがって、[!INCLUDE[ssSB](../../includes/sssb-md.md)] では削除対象のコントラクトを使用するサービスとの新しいメッセージ交換は許可されません。 このコントラクトを使用する既存のメッセージ交換に影響はありません。  
  
 サービスの AUTHORIZATION を変更するには、ALTER AUTHORIZATION ステートメントを使用します。  
  
## <a name="permissions"></a>アクセス許可  
 サービスを変更する権限は、既定では、サービスの所有者、**db_ddladmin** または **db_owner** 固定データベース ロールのメンバー、および **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>例  
  
### <a name="a-changing-the-queue-for-a-service"></a>A. サービスのキューを変更する  
 次の例では、キュー `//Adventure-Works.com/Expenses` を使用するよう、`NewQueue` サービスを変更します。  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE NewQueue ;  
```  
  
### <a name="b-adding-a-new-contract-to-the-service"></a>B. サービスに新しいコントラクトを追加する  
 次の例では、コントラクト `//Adventure-Works.com/Expenses` のダイアログを許可するよう、`//Adventure-Works.com/Expenses` サービスを変更します。  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="c-adding-a-new-contract-to-the-service-dropping-existing-contract"></a>C. サービスに新しいコントラクトを追加し、既存のコントラクトを削除する  
 次の例では、コントラクト `//Adventure-Works.com/Expenses` のダイアログを許可し、コントラクト `//Adventure-Works.com/Expenses/ExpenseProcessing` のダイアログを禁止するよう、`//Adventure-Works.com/Expenses/ExpenseSubmission` サービスを変更します。  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing],   
     DROP CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
