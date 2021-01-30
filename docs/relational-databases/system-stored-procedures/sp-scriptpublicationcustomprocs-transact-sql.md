---
description: sp_scriptpublicationcustomprocs (Transact-SQL)
title: sp_scriptpublicationcustomprocs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 733ca066ba7c11754fde7b82b228c7ac3796a42e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99189967"
---
# <a name="sp_scriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  自動生成カスタムプロシージャスキーマオプションが有効になっているパブリケーション内のすべてのテーブルアーティクルに対して、カスタムの INSERT、UPDATE、および DELETE プロシージャをスクリプト化します。 **sp_scriptpublicationcustomprocs** は、スナップショットが手動で適用されるサブスクリプションを設定する場合に特に便利です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication_name'` パブリケーションの名前を指定します。 *publication_name* は **sysname** で、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 1つの **nvarchar (4000)** 列で構成される結果セットを返します。 この結果セットは、カスタム ストアド プロシージャの作成に必要な、完全な CREATE PROCEDURE ステートメントを構成します。  
  
## <a name="remarks"></a>コメント  
 カスタムプロシージャは、自動生成カスタムプロシージャ (0x2) スキーマオプションを指定しないと、アーティクルに対してスクリプト化されません。  
  
 次の手順は、 **sp_scriptpublicationcustomprocs** がサブスクライバーのプロシージャを作成するために使用します。このプロシージャを直接実行することはできません。  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>アクセス許可  
 実行権限が **public** に付与されます。このストアドプロシージャ内で手続き型のセキュリティチェックが実行され、 **sysadmin** 固定サーバーロールのメンバーと、現在のデータベースの固定データベースロール **db_owner** のメンバーへのアクセスが制限されます。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
