---
description: sp_resyncmergesubscription (Transact-sql)
title: sp_resyncmergesubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 86e1aaf4ee97447518e09a9b0b08a2624015cbef
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540486"
---
# <a name="sp_resyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定した既知の検証状態にマージサブスクリプションを再同期します。 これによって、サブスクリプション データベースを、正常終了した前回の検証時や指定の日時など、特定の時点に強制的に集約または同期できます。 この方法を使用してサブスクリプションを再同期する場合、スナップショットは再適用されません。 このストアド プロシージャは、スナップショット レプリケーション サブスクリプションまたはトランザクション レプリケーション サブスクリプションでは使用しません。 このストアドプロシージャは、パブリッシャー、パブリケーションデータベース、またはサブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_resyncmergesubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @resync_type = ] resync_type ]  
    [ , [ @resync_date_str = ] resync_date_string ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値は NULL です。 ストアドプロシージャがパブリッシャーで実行されている場合は、NULL 値が有効です。 ストアド プロシージャをサブスクライバー側で実行する場合は、パブリッシャーを指定する必要があります。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーションデータベースの名前を指定します。 *publisher_db* は **sysname**,、既定値は NULL です。 NULL の値は、ストアドプロシージャがパブリッシャー側のパブリケーションデータベースで実行されている場合に有効です。 ストアド プロシージャをサブスクライバー側で実行する場合は、パブリッシャーを指定する必要があります。  
  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication*は **sysname**,、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* の **sysname**,、既定値は NULL です。 NULL の値は、ストアドプロシージャがサブスクライバーで実行されている場合に有効です。 ストアドプロシージャをパブリッシャーで実行する場合は、サブスクライバーを指定する必要があります。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプションデータベースの名前を指定します。 *subscription_db* は **sysname**,、既定値は NULL です。 ストアド プロシージャをサブスクリプション データベースのサブスクライバー側で実行する場合は、NULL の値が有効です。 ストアドプロシージャをパブリッシャーで実行する場合は、サブスクライバーを指定する必要があります。  
  
`[ @resync_type = ] resync_type` 再同期が開始されるタイミングを定義します。 *resync_type* は **int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|初期スナップショットの後から同期が開始されます。 初期スナップショット以降のすべての変更がサブスクライバーに再適用されるため、これは最もリソースを大量に消費するオプションです。|  
|**1**|前回の検証が正常に完了した後に同期が開始されます。 最後に検証が正常に完了した後に発生した、新規または不完全なすべてのジェネレーションがサブスクライバーに再適用されます。|  
|**2**|同期は、 *resync_date_str*で指定された日付から開始されます。 指定の日付以降の、すべての新しい生成結果または完了していない生成結果がサブスクライバーに再適用されます。|  
  
`[ @resync_date_str = ] resync_date_string` 再同期を開始する日付を定義します。 *resync_date_string* は **nvarchar (30)**,、既定値は NULL です。 このパラメーターは、 *resync_type* の値が **2**の場合に使用されます。 指定された日付は、対応する **datetime** 値に変換されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_resyncmergesubscription** は、マージレプリケーションで使用します。  
  
 *Resync_type*パラメーターの値が**0**の場合、初期スナップショット以降のすべての変更が再適用されますが、リソースを大量に消費する可能性がありますが、完全な再初期化よりもかなり少なくなる可能性があります。 たとえば、初期スナップショットが1か月前に配信された場合、この値によって過去1か月のデータが再適用されます。 初期スナップショットに 1 gb のデータが含まれていても、過去1か月の変更量が2メガバイト (MB) の変更されたデータである場合は、1 GB の完全なスナップショットを再適用するよりもデータを再適用する方が効率的です。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_resyncmergesubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
