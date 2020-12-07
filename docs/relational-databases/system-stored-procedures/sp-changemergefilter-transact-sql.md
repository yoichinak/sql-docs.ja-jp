---
description: sp_changemergefilter (Transact-SQL)
title: sp_changemergefilter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergefilter_TSQL
- sp_changemergefilter
helpviewer_keywords:
- sp_changemergefilter
ms.assetid: e08fdfdd-d242-4e85-817b-9f7a224fe567
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3e5a5208eeb1a47971e1960bd9c9c581d5d6517e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539127"
---
# <a name="sp_changemergefilter-transact-sql"></a>sp_changemergefilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  一部のマージフィルタープロパティを変更します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changemergefilter [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
        , [ @filtername= ] 'filtername'  
        , [ @property= ] 'property'  
        , [ @value= ] 'value'  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` アーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値はありません。  
  
`[ @filtername = ] 'filtername'` フィルターの現在の名前を指定します。 *filtername* は **sysname**,、既定値はありません。  
  
`[ @property = ] 'property'` 変更するプロパティの名前を指定します。 *プロパティ* は **sysname**,、既定値はありません。  
  
`[ @value = ] 'value'` 指定したプロパティの新しい値を指定します。 *値*は **nvarchar (1000)**,、既定値はありません。  
  
 次の表では、アーティクルのプロパティとそれらのプロパティの値について説明します。  
  
|プロパティ|[値]|説明|  
|--------------|-----------|-----------------|  
|**filter_type**|**1**|結合フィルター。<br /><br /> このオプションは、サブスクライバーをサポートするために必要です [!INCLUDE[ssEW](../../includes/ssew-md.md)] 。|  
||**2**|論理レコードリレーションシップ。|  
||**3**|結合フィルターは論理レコードリレーションシップでもあります。|  
|**filtername**||フィルターの名前。|  
|**join_articlename**||結合アーティクルの名前。|  
|**join_filterclause**||フィルター句。|  
|**join_unique_key**|**true**|結合は、一意なキーに基づいて行われます。|  
||**false**|結合が一意のキーではありません。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot* は **ビット**であり、既定値は **0**です。  
  
 **0** を指定すると、マージアーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1** に設定すると、マージアーティクルへの変更によってスナップショットが無効になる可能性があります。また、新しいスナップショットを必要とする既存のサブスクリプションが存在する場合は、既存のスナップショットに古いスナップショットとしてマークを付け、新しいスナップショットを生成する権限を与えます。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription* は **ビット** で、既定値は **0**です。  
  
 **0** を指定すると、マージアーティクルへの変更によってサブスクリプションが再初期化されることはありません。 変更によって既存のサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1** を指定すると、マージアーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changemergefilter** は、マージレプリケーションで使用します。  
  
 マージアーティクルのフィルターを変更するには、スナップショットが存在する場合は再作成する必要があります。 これを行うには、 ** \@ force_invalidate_snapshot**を**1**に設定します。 また、この記事へのサブスクリプションがある場合は、サブスクリプションを再初期化する必要があります。 これを行うには、 ** \@ force_reinit_subscription**を**1**に設定します。  
  
 論理レコードを使用するには、パブリケーションとアーティクルが多くの要件を満たしている必要があります。 詳細については、「[Group Changes to Related Rows with Logical Records](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」 (論理レコードによる関連行への変更のグループ化) を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changemergefilter**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_dropmergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
