---
description: sp_helparticlecolumns (Transact-SQL)
title: sp_helparticlecolumns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_helparticlecolumns
- sp_helparticlecolumns_TSQL
helpviewer_keywords:
- sp_helparticlecolumns
ms.assetid: 9ea55df3-2e99-4683-88ad-bde718288bc7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 96e4f5508af16314312d2add0a7cdb8dd07a3921
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99176473"
---
# <a name="sp_helparticlecolumns-transact-sql"></a>sp_helparticlecolumns (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  基になるテーブルのすべての列を返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。 Oracle パブリッシャーの場合、このストアドプロシージャは、ディストリビューター側の任意のデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helparticlecolumns [ @publication = ] 'publication'   
        , [ @article = ] 'article'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルを含むパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` 返される列が含まれているアーティクルの名前を指定します。 *アーティクル* は **sysname** で、既定値はありません。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname** で、既定値は NULL です。  
  
> [!NOTE]  
>  要求されたアーティクルがパブリッシャーによってパブリッシュされている場合、*パブリッシャー* を指定することはできません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (パブリッシュされていない列) または **1** (パブリッシュされた列)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**列 id**|**int**|列の識別子です。|  
|**column**|**sysname**|列の名前です。|  
|**投稿**|**bit**|列をパブリッシュしたかどうかを示します。<br /><br /> **0** = いいえ<br /><br /> **1** = はい|  
|**パブリッシャーの種類**|**sysname**|パブリッシャー側の列のデータ型。|  
|**サブスクライバーの種類**|**sysname**|サブスクライバー側の列のデータ型。|  
  
## <a name="remarks"></a>コメント  
 **sp_helparticlecolumns** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 **sp_helparticlecolumns** は、列方向のパーティションをチェックする場合に便利です。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helparticlecolumns** を実行できるのは、 **sysadmin** 固定サーバーロールのメンバー、 **db_owner** 固定データベースロールのメンバー、または現在のパブリケーションのパブリケーションアクセスリストのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [列フィルターを定義および変更する](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_droppublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
