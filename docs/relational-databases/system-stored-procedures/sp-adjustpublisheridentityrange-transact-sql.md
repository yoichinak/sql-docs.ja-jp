---
description: sp_adjustpublisheridentityrange (Transact-SQL)
title: sp_adjustpublisheridentityrange (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adjustpublisheridentityrange_TSQL
- sp_adjustpublisheridentityrange
helpviewer_keywords:
- sp_adjustpublisheridentityrange
ms.assetid: 64f111fd-fb7d-4459-93f7-65f0f8dd7efe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cdb8f12f5c5ff3c3c01f5d7cd18827b2fec0e9c8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541987"
---
# <a name="sp_adjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パブリケーションの ID 範囲を調整し、パブリケーションのしきい値に基づいて新しい範囲を再割り当てします。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 新しい id 範囲が再割り当てされるパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値は NULL です。  
  
`[ @table_name = ] 'table_name'` 新しい id 範囲が再割り当てされるテーブルの名前を指定します。 *table_name* は **sysname**,、既定値は NULL です。  
  
`[ @table_owner = ] 'table_owner'` パブリッシャーのテーブルの所有者を示します。 *table_owner* は **sysname**,、既定値は NULL です。 *Table_owner*が指定されていない場合は、現在のユーザーの名前が使用されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_adjustpublisheridentityrange** は、すべての種類のレプリケーションで使用されます。  
  
 自動 ID 範囲が有効になっているパブリケーションの場合は、ディストリビューション エージェントまたはマージ エージェントが、パブリケーションのしきい値に基づいてパブリケーションの ID 範囲を自動的に調整します。 ただし、何らかの理由でディストリビューションエージェントまたはマージエージェントが一定期間実行されていない場合や、id 範囲のリソースがしきい値のポイントまで頻繁に使用されている場合、ユーザーは **sp_adjustpublisheridentityrange** を呼び出して、パブリッシャーの新しい範囲の値を割り当てることができます。  
  
 **Sp_adjustpublisheridentityrange**の実行時には、 *publication*または*table_name*のいずれかを指定する必要があります。 またはの両方が指定されていない場合は、エラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_adjustpublisheridentityrange**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
