---
description: sp_reinitmergesubscription (Transact-sql)
title: sp_reinitmergesubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergesubscription_TSQL
- sp_reinitmergesubscription
helpviewer_keywords:
- sp_reinitmergesubscription
ms.assetid: 249a4048-e885-48e0-a92a-6577f59de751
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bc1d2d3dc8b9763d19410b2a9773fb7766d22140
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364745"
---
# <a name="sp_reinitmergesubscription-transact-sql"></a>sp_reinitmergesubscription (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージ エージェントの次回実行時に再初期化するように、マージ サブスクリプションにマークを付けます。 このストアドプロシージャは、パブリッシャー側のパブリケーションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_reinitmergesubscription [ [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber'  
    [ , [ @subscriber_db = ] 'subscriber_db'  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname** ,、既定値は **all** です。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* は **sysname** ,、既定値は **all** です。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクライバーデータベースの名前を指定します。 *subscriber_db* は **sysname** で、既定値は **all** です。  
  
`[ @upload_first = ] 'upload_first'` サブスクリプションを再初期化する前に、サブスクライバーでの変更をアップロードするかどうかを指定します。 *upload_first* は **nvarchar (5)** ,、既定値は FALSE です。 **True** の場合、サブスクリプションが再初期化される前に変更がアップロードされます。 **False** の場合、変更はアップロードされません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>注釈  
 **sp_reinitmergesubscription** は、マージレプリケーションで使用します。  
  
 **sp_reinitmergesubscription** は、マージサブスクリプションを再初期化するためにパブリッシャーから呼び出すことができます。 スナップショットエージェントも再実行することをお勧めします。  
  
 パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
## <a name="examples"></a>例  

### <a name="a-reinitialize-the-push-subscription-and-lose-pending-changes"></a>A. プッシュサブスクリプションを再初期化して保留中の変更を破棄する

 [!code-sql[HowTo#sp_reinitmergepushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_1.sql)]  
  
### <a name="b-reinitialize-the-push-subscription-and-upload-pending-changes"></a>B. プッシュサブスクリプションを再初期化し、保留中の変更をアップロードします
 [!code-sql[HowTo#sp_reinitmergepushsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_2.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_reinitmergesubscription** を実行できるのは、固定サーバーロール **sysadmin** または固定データベースロール **db_owner** のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
