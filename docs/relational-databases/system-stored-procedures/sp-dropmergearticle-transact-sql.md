---
description: sp_dropmergearticle (Transact-SQL)
title: sp_dropmergearticle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergearticle
- sp_dropmergearticle_TSQL
helpviewer_keywords:
- sp_dropmergearticle
ms.assetid: 5ef1fbf7-c03d-4488-9ab2-64aae296fa4f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7c91fe7b1cc57630565fae398fc8cbc798df314a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536531"
---
# <a name="sp_dropmergearticle-transact-sql"></a>sp_dropmergearticle (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  アーティクルをマージ パブリケーションから削除します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropmergearticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'   
    [ , [ @ignore_distributor= ] ignore_distributor   
    [ , [ @reserved= ] reserved   
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルを削除するパブリケーションの名前を指定します。 *publication*は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` 指定したパブリケーションから削除するアーティクルの名前を指定します。 *アーティクル*は **sysname**で、既定値はありません。 **All**の場合、指定されたマージパブリケーションの既存のアーティクルはすべて削除されます。 *Article*が**all**の場合でも、パブリケーションはアーティクルとは別に削除する必要があります。  
  
`[ @ignore_distributor = ] ignore_distributor` ディストリビューターに接続せずにこのストアドプロシージャを実行するかどうかを示します。 *ignore_distributor* は **ビット**,、既定値は **0**です。  
  
`[ @reserved = ] reserved` 将来使用するために予約されています。 *予約済み* は **nvarchar (20)**,、既定値は NULL です。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` スナップショットを無効にする機能を有効または無効にします。 *force_invalidate_snapshot* は **ビット**であり、既定値は **0**です。  
  
 **0** を指定すると、マージアーティクルへの変更によってスナップショットが無効になることはありません。  
  
 **1** に設定すると、マージアーティクルへの変更によってスナップショットが無効になる可能性があります。この場合、値 **1** を指定すると、新しいスナップショットを作成する権限が与えられます。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` アーティクルを削除する際に、既存のサブスクリプションを再初期化する必要があることを確認します。 *force_reinit_subscription* は **ビット**,、既定値は **0**です。  
  
 **0** を指定すると、アーティクルを削除してもサブスクリプションが再初期化されません。  
  
 **1** を指定すると、アーティクルを削除すると既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` 内部でのみ使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_dropmergearticle** は、マージレプリケーションで使用します。 アーティクルの削除の詳細については、「 [既存のパブリケーションのアーティクルの追加および削除](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)」を参照してください。  
  
 **Sp_dropmergearticle**を実行してパブリケーションからアーティクルを削除しても、パブリケーションデータベースからオブジェクトが削除されたり、サブスクリプションデータベースから対応するオブジェクトが削除されることはありません。 必要であれば `DROP <object>` を使用して、手動でこれらのオブジェクトを削除します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_dropmergearticle**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="example"></a>例  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @table1 AS sysname;  
DECLARE @table2 AS sysname;  
DECLARE @table3 AS sysname;  
DECLARE @salesschema AS sysname;  
DECLARE @hrschema AS sysname;  
DECLARE @filterclause AS nvarchar(1000);  
SET @publication = N'AdvWorksSalesOrdersMerge';   
SET @table1 = N'Employee';   
SET @table2 = N'SalesOrderHeader';   
SET @table3 = N'SalesOrderDetail';   
SET @salesschema = N'Sales';  
SET @hrschema = N'HumanResources';  
SET @filterclause = N'Employee.LoginID = HOST_NAME()';  
  
-- Drop the merge join filter between SalesOrderHeader and SalesOrderDetail.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table3,   
  @filtername = N'SalesOrderDetail_SalesOrderHeader',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the merge join filter between Employee and SalesOrderHeader.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table2,   
  @filtername = N'SalesOrderHeader_Employee',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderDetail table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table3,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderHeader table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table2,   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the Employee table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table1,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [アーティクルの削除](../../relational-databases/replication/publish/delete-an-article.md)   
 [既存のパブリケーションでのアーティクルの追加と削除](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
