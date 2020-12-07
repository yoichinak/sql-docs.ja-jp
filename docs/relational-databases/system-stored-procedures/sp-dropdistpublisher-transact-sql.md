---
description: sp_dropdistpublisher (Transact-sql)
title: sp_dropdistpublisher (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2d7d0eed28b877c881cd297556755ea70bf5c674
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543519"
---
# <a name="sp_dropdistpublisher-transact-sql"></a>sp_dropdistpublisher (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  ディストリビューションパブリッシャーを削除します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` 削除するパブリッシャーを示します。 *publisher* は **sysname**で、既定値はありません。  
  
`[ @no_checks = ] no_checks` パブリッシャーがディストリビューターとしてサーバーをアンインストールしたかどうかを **sp_dropdistpublisher** に確認するかどうかを指定します。 *no_checks* は **ビット**,、既定値は **0**です。  
  
 **0**の場合、レプリケーションは、リモートパブリッシャーがローカルサーバーをディストリビューターとしてアンインストールしたことを確認します。 パブリッシャーがローカルの場合、レプリケーションでは、ローカルサーバーにパブリケーションまたはディストリビューションオブジェクトが残っていないことを確認します。  
  
 **1**の場合、リモートパブリッシャーに到達できない場合でも、ディストリビューションパブリッシャーに関連付けられているすべてのレプリケーションオブジェクトが削除されます。 この操作を行った後、リモートパブリッシャーは、 ** \@ ignore_distributor**1 の[sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)を使用してレプリケーションをアンインストールする必要があり  =  **1**ます。  
  
`[ @ignore_distributor = ] ignore_distributor` パブリッシャーが削除されたときに、ディストリビューターにディストリビューションオブジェクトを残すかどうかを指定します。 *ignore_distributor* は **ビット** で、次のいずれかの値を指定できます。  
  
 **1** = *パブリッシャー* に属するディストリビューションオブジェクトは、ディストリビューターで保持されます。  
  
 **0** = *パブリッシャー* のディストリビューションオブジェクトは、ディストリビューターでクリーンアップされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_dropdistpublisher** は、すべての種類のレプリケーションで使用されます。  
  
 Oracle パブリッシャーを削除できない場合は、パブリッシャーを削除できないと **sp_dropdistpublisher** によってエラーが返され、パブリッシャーのディストリビューターオブジェクトが削除されます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_dropdistpublisher**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [パブリッシングおよびディストリビューションの無効化](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
