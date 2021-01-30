---
description: sp_helpmergealternatepublisher (Transact-sql)
title: sp_helpmergealternatepublisher (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_helpmergealternatepublisher_TSQL
- sp_helpmergealternatepublisher
helpviewer_keywords:
- sp_helpmergealternatepublisher
ms.assetid: a96e365f-5967-4580-9d79-5bacf2d12211
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e7448059958f07ba1aab7e63a1a857e113e21432
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99183103"
---
# <a name="sp_helpmergealternatepublisher-transact-sql"></a>sp_helpmergealternatepublisher (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージパブリケーションの代替パブリッシャーとして有効なすべてのサーバーの一覧を返します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergealternatepublisher [ @publisher = ] 'publisher', [ @publisher_db = ] 'publisher_db', [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` 代替パブリッシャーの名前を指定します。*publisher* は **sysname** で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーションデータベースの名前を指定します。*publisher_db* は **sysname** であり、既定値はありません。  
  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。*publication* は **sysname**,、既定値はありません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**alternate_publisher**|**sysname**|代替パブリッシャーの名前です。|  
|**alternate_publisher_db**|**sysname**|パブリケーションデータベースの名前。|  
|**alternate_publication**|**sysname**|パブリケーションの名前。|  
|**alternate_distributor**|**sysname**|ディストリビューターの名前。|  
|**friendly_name**|**nvarchar (255)**|代替パブリッシャーの説明。|  
|**有効**|**bit**|サーバーが代替パブリッシャーかどうかを示します。 **1** は、パブリッシャーが代替パブリッシャーとして有効になっていることを示します。 **0** は、有効になっていないことを示します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpmergealternatepublisher** は、マージレプリケーションで使用します。  
  
 マージ セッションごとに、システムではパブリッシャーとサブスクライバーの両方に対し、代替パブリッシャーの一覧を求めるクエリが実行されます。 マージ処理では代替パブリッシャーの一覧に対してエントリの追加や削除が行われ、サブスクライバーとパブリッシャーの両方に一致する代替パブリッシャーの一覧が生成されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpmergealternatepublisher** を実行できるのは、パブリケーションのパブリケーションアクセスリストのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
