---
description: sp_enumeratependingschemachanges (Transact-SQL)
title: sp_enumeratependingschemachanges (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a75e22f94688d4d8819b22b1b478bd3a3a66ce1
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99193568"
---
# <a name="sp_enumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  保留中のすべてのスキーマ変更に関する一覧を返します。 このストアドプロシージャは、 [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)と共に使用できます。これにより、管理者は、選択した保留中のスキーマ変更をスキップして、レプリケートされないようにすることができます。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @starting_schemaversion = ] starting_schemaversion` 結果セットに含めるスキーマ変更の最小数を指定します。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|スキーマ変更が適用されるアーティクルの名前、またはパブリケーション全体に適用されるスキーマ変更の場合は **パブリケーション全体** 。|  
|**schemaversion**|**int**|保留中のスキーマ変更の数。|  
|**schematype**|**sysname**|スキーマ変更の種類を表すテキスト値。|  
|**スキーマのスキーマ**|**nvarchar(max)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] スキーマの変更について説明します。|  
|**schemastatus**|**nvarchar (10)**|スキーマ変更がアーティクルに対して保留になっているかどうかを示します。次のいずれかの値をとります。<br /><br /> **active** = スキーマの変更は保留中です<br /><br /> **inactive** = スキーマ変更が非アクティブ<br /><br /> **skip** = スキーマの変更はレプリケートされません|  
|**schemaguid**|**uniqueidentifier**|スキーマの変更を識別します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_enumeratependingschemachanges** は、マージレプリケーションで使用します。  
  
 [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)と共に使用される **sp_enumeratependingschemachanges** は、マージレプリケーションのサポートを目的としており、再初期化などの他の是正措置によって状況を修正できなかった場合にのみ使用してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_enumeratependingschemachanges** を実行できるのは、固定サーバーロール **sysadmin** または固定データベースロール **db_owner** のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sysmergeschemachange &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
