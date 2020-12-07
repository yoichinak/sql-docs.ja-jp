---
description: sp_addmergepartition (Transact-sql)
title: sp_addmergepartition (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6ffb754208c6923a625860ba3c22bd9dc88e466d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546333"
---
# <a name="sp_addmergepartition-transact-sql"></a>sp_addmergepartition (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  サブスクライバーで [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) または [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) の値によってフィルター処理されたサブスクリプションに対して、動的にフィルター選択されたパーティションを作成します。 このストアド プロシージャは、パブリッシュされるデータベース上のパブリッシャー側で実行されるもので、手動でパーティションを生成する場合に使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パーティションが作成されるマージパブリケーションを指定します。 *publication* は **sysname**,、既定値はありません。 *Suser_sname*が指定されている場合、 *hostname*の値は NULL である必要があります。  
  
`[ @suser_sname = ] 'suser_sname'` サブスクライバー側の [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 関数の値によってフィルター処理されるサブスクリプションのパーティションを作成するときに使用する値を指定します。 *suser_sname* は **sysname**であり、既定値はありません。  
  
`[ @host_name = ] 'host_name'` サブスクライバー側の [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 関数の値によってフィルター処理されるサブスクリプションのパーティションを作成するときに使用する値を指定します。 *host_name* は **sysname**であり、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_addmergepartition** は、マージレプリケーションで使用します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addmergepartition**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [パラメーター化されたフィルターを使用してマージパブリケーションのスナップショットを作成する](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [パラメーター化された行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
