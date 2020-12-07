---
description: sp_mergecleanupmetadata (Transact-sql)
title: sp_mergecleanupmetadata (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6f23cb729b98865b6dce4d15dcde555193d313eb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546026"
---
# <a name="sp_mergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 より前のバージョンのを実行しているサーバーを含むレプリケーショントポロジでのみ使用してください。**sp_mergecleanupmetadata** を使用すると、管理者は、 **MSmerge_genhistory**、 **MSmerge_contents** および **MSmerge_tombstone** システムテーブル内のメタデータをクリーンアップできます。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* のデータ型は **sysname**で、既定値はです **%** 。これにより、すべてのパブリケーションのメタデータがクリーンアップされます。 明示的に指定した場合、パブリケーションは既に存在している必要があります。  
  
`[ @reinitialize_subscriber = ] 'subscriber'` サブスクライバーを再初期化するかどうかを指定します。 *サブスクライバー* は **nvarchar (5)**,、 **true** または **FALSE**,、既定値は **true**です。 **TRUE**の場合、サブスクリプションに再初期化のマークが付けられます。 **FALSE**の場合、サブスクリプションには再初期化のマークが付けられません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_mergecleanupmetadata** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 1 より前のバージョンのを実行しているサーバーを含むレプリケーショントポロジでのみ使用してください [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 。 Service Pack 1 以降のみを含むトポロジでは、 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 自動保有期間に基づくメタデータのクリーンアップを使用する必要があります。 このストアド プロシージャを実行する場合は、実行するコンピューター上で、きわめて大きいログファイルが必要であり、作成される可能性があることに注意してください。  
  
> [!CAUTION]
>  **Sp_mergecleanupmetadata**の実行後、既定では、 **MSmerge_genhistory**、 **MSmerge_contents**および**MSmerge_tombstone**にメタデータが格納されているパブリケーションのサブスクライバーのすべてのサブスクリプションは再初期化のマークが付けられ、サブスクライバーでの保留中の変更はすべて失われ、現在のスナップショットは古い形式に設定されます。  
> 
> [!NOTE]
>  データベースに複数のパブリケーションが存在し、それらのパブリケーションのいずれかが無期限のパブリケーション保有期間 (** \@ リテンション**0) を使用している場合 = **0**は、 **sp_mergecleanupmetadata**を実行しても、データベースのマージレプリケーション変更追跡メタデータはクリーンアップされません。 このため、無期限のパブリケーション保有期間は注意して使用してください。  
  
 このストアドプロシージャを実行するときに、 ** \@ reinitialize_subscriber**パラメーターを**TRUE** (既定値) または**FALSE**に設定して、サブスクライバーを再初期化するかどうかを選択できます。 ** \@ Reinitialize_subscriber**パラメーターを**TRUE**に設定して**sp_mergecleanupmetadata**を実行すると、初期スナップショットを使用せずにサブスクリプションが作成された場合でも、サブスクライバーでスナップショットが再適用されます (スナップショットデータとスキーマが手動で適用された場合や、サブスクライバーに既に存在していた場合など)。 パラメーターを **FALSE** に設定する場合は、注意してください。パブリケーションが再初期化されない場合は、パブリッシャーとサブスクライバーのデータが同期されていることを確認する必要があります。  
  
 ** \@ Reinitialize_subscriber**の値に関係なく、ストアドプロシージャが呼び出されたときに、パブリッシャーまたは再パブリッシュサブスクライバーに変更をアップロードしようとしている進行中のマージプロセスがある場合、 **sp_mergecleanupmetadata**は失敗します。  
  
 **Reinitialize_subscriber を TRUE にして sp_mergecleanupmetadata を実行する \@ :**  
  
1.  パブリケーションデータベースとサブスクリプションデータベースに対するすべての更新を停止することをお勧めしますが、必須ではありません。 更新が続行された場合、パブリケーションが再初期化されると、前回のマージ以降にサブスクライバーで行われた更新は失われますが、データの収束が維持されます。  
  
2.  マージ エージェントを実行してマージを実行します。 マージエージェントを実行するときは、各サブスクライバーで **-Validate** agent コマンドラインオプションを使用することをお勧めします。 連続モードのマージを実行する場合は、このセクションで後述する「 *連続モードのマージに関する特別な考慮事項* 」を参照してください。  
  
3.  すべてのマージが完了したら、 **sp_mergecleanupmetadata**を実行します。  
  
4.  名前付きまたは匿名のプルサブスクリプションを使用してすべてのサブスクライバーで **sp_reinitmergepullsubscription** を実行し、データの収束を保証します。  
  
5.  連続モードのマージを実行する場合は、このセクションで後述する「 *連続モードのマージに関する特別な考慮事項* 」を参照してください。  
  
6.  すべてのレベルで関係するすべてのマージ パブリケーションに対して、スナップショット ファイルを再生成します。 最初にスナップショットを再生成せずにマージしようとすると、スナップショットを再生成するように要求されます。  
  
7.  パブリケーション データベースをバックアップします。 この操作を行わないと、パブリケーションデータベースの復元後にマージエラーが発生する可能性があります。  
  
 **Reinitialize_subscriber = FALSE を使用して sp_mergecleanupmetadata を実行してい \@ ます:**  
  
1.  パブリケーションデータベースとサブスクリプションデータベースに対する **すべて** の更新を停止します。  
  
2.  マージ エージェントを実行してマージを実行します。 マージエージェントを実行するときは、各サブスクライバーで **-Validate** agent コマンドラインオプションを使用することをお勧めします。 連続モードのマージを実行する場合は、このセクションで後述する「 *連続モードのマージに関する特別な考慮事項* 」を参照してください。  
  
3.  すべてのマージが完了したら、 **sp_mergecleanupmetadata**を実行します。  
  
4.  連続モードのマージを実行する場合は、このセクションで後述する「 *連続モードのマージに関する特別な考慮事項* 」を参照してください。  
  
5.  すべてのレベルで関係するすべてのマージ パブリケーションに対して、スナップショット ファイルを再生成します。 最初にスナップショットを再生成せずにマージしようとすると、スナップショットを再生成するように要求されます。  
  
6.  パブリケーション データベースをバックアップします。 この操作を行わないと、パブリケーションデータベースの復元後にマージエラーが発生する可能性があります。  

 **連続モードのマージに関する注意事項**  
  
 連続モードのマージを実行する場合は、次のいずれかを行う必要があります。  
  
-   マージエージェントを停止し、 **-Continuous** パラメーターを指定せずに別のマージを実行します。  
  
-   パブリケーションの状態をポーリングする連続モードのマージが失敗するように、 **sp_changemergepublication** でパブリケーションを非アクティブ化します。  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 **Sp_mergecleanupmetadata**の実行の手順3を完了したら、停止した方法に基づいて連続モードのマージを再開します。 次のいずれか:  
  
-   マージエージェントに対して、 **-Continuous** パラメーターを再び追加します。  
  
-   Sp_changemergepublication でパブリケーションを再アクティブ化 **します。**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_mergecleanupmetadata**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
 このストアド プロシージャを使用するには、パブリッシャーが [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] を実行していることが必要です。 サブスクライバーで [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] は、または [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 Service Pack 2 が実行されている必要があります。  
  
## <a name="see-also"></a>参照  
 [MSmerge_genhistory &#40;Transact-sql&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-sql&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact-sql&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
