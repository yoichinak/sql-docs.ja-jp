---
description: sp_removedistpublisherdbreplication (Transact-SQL)
title: sp_removedistpublisherdbreplication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1d249b6d22b38bbfe986e2f2ba3d2dba120ce4a5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99206458"
---
# <a name="sp_removedistpublisherdbreplication-transact-sql"></a>sp_removedistpublisherdbreplication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  ディストリビューター側の特定のパブリケーションに属するパブリッシュ メタデータを削除します。 このストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーサーバーの名前を指定します。 *publisher* は **sysname** で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーションデータベースの名前を指定します。 *publisher_db* は **sysname** で、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_removedistpublisherdbreplication** は、トランザクションレプリケーションとスナップショットレプリケーションで使用されます。  
  
 **sp_removedistpublisherdbreplication** は、ディストリビューションデータベースを削除せずにパブリッシュされたデータベースを再作成する必要がある場合に使用します。 次のメタデータが削除されます。  
  
-   すべてのパブリケーション メタデータ  
  
-   そのパブリケーションに属するすべてのアーティクルのメタデータ  
  
-   パブリケーションに対するすべてのサブスクリプションのメタデータ。  
  
-   パブリケーションに属するすべてのレプリケーションエージェントジョブのメタデータ。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_removedistpublisherdbreplication** を実行できるのは、ディストリビューター側の固定サーバーロール **sysadmin** のメンバー、またはディストリビューションデータベース内の **db_owner** 固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
