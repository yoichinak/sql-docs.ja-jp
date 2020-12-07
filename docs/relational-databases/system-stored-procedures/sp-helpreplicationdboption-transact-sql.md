---
description: sp_helpreplicationdboption (Transact-sql)
title: sp_helpreplicationdboption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6733b1f473c91094bd8af177bce4b13f3cf1b03e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89527053"
---
# <a name="sp_helpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  パブリッシャー側のデータベースでレプリケーションが有効になっているかどうかを示します。 このストアドプロシージャは、パブリッシャー側で任意のデータベースに対して実行されます。 *Oracle パブリッシャーではサポートされていません。*  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'dbname'` データベースの名前を指定します。 *dbname* は **sysname**,、既定値は **%** です。 の場合、 **%** 結果セットにはパブリッシャーのすべてのデータベースが含まれます。それ以外の場合は、指定されたデータベースに関する情報のみが返されます。 次に示すように、ユーザーが適切な権限を持っていないデータベースについては、情報は返されません。  
  
`[ @type = ] 'type'` 指定されたレプリケーションオプションの *種類* の値が有効になっているデータベースのみが含まれるように結果セットを制限します。 *種類* は **sysname**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**投稿**|トランザクションレプリケーションを許可します。|  
|**merge publish**|マージレプリケーションが許可されています。|  
|**レプリケーションが許可され** ている (既定)|トランザクション レプリケーションまたはマージ レプリケーションを許可します。|  
  
`[ @reserved = ] reserved` 既存のパブリケーションとサブスクリプションに関する情報を返すかどうかを指定します。 *予約済み* の **ビット**,、既定値は0です。 **1**の場合、結果セットには、指定されたデータベースに既存のパブリケーションまたはサブスクリプションがあるかどうかに関する情報が含まれます。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|データベースの名前です。|  
|**id**|**int**|データベース識別子。|  
|**transpublish**|**bit**|データベースでスナップショットまたはトランザクションパブリッシングが有効になっている場合は、値が **1** の場合は、スナップショットパブリケーションまたはトランザクションパブリッシングが有効であることを示します。|  
|**mergepublish**|**bit**|データベースでマージパブリッシングが有効になっている場合は、値が **1** の場合は、マージパブリッシングが有効であることを示します。|  
|**dbowner**|**bit**|ユーザーが **db_owner** 固定データベースロールのメンバーである場合は、値が **1** の場合は、ユーザーがこのロールのメンバーであることを示します。|  
|**dbreadonly**|**bit**|データベースが読み取り専用としてマークされているかどうかを示します。値が **1** の場合は、データベースが読み取り専用であることを意味します。|  
|**haspublications**|**bit**|データベースに既存のパブリケーションがあるかどうかを示します。値が **1** の場合は、既存のパブリケーションが存在することを意味します。|  
|**haspullsubscriptions**|**bit**|データベースに既存のプルサブスクリプションがあるかどうかを示します。値が **1** の場合は、既存のプルサブスクリプションが存在することを意味します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpreplicationdboption** は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーは、任意のデータベースに対して**sp_helpreplicationdboption**を実行できます。 **Db_owner**固定データベースロールのメンバーは、そのデータベースの**sp_helpreplicationdboption**を実行できます。  
  
## <a name="see-also"></a>参照  
 [sp_replicationdboption &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
