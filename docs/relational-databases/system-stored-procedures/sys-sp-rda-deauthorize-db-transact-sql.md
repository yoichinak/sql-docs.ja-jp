---
title: sys.sp_rda_deauthorize_db (Transact-sql) |Microsoft Docs
description: Sys.sp_rda_deauthorize_db を使用して、ローカル Stretch 対応データベースとリモート Azure データベース間の認証された接続を削除する方法について説明します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9abdf527c434674ccecd655c93c27606b29b940d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99186638"
---
# <a name="syssp_rda_deauthorize_db-transact-sql"></a>sys.sp_rda_deauthorize_db (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  ローカル Stretch 対応データベースとリモート Azure データベース間の認証された接続を削除します。 リモートデータベースにアクセスできない場合、またはデータベース内のすべての Stretch 対応テーブルのクエリ動作を変更する場合は、 **sp_rda_deauthorize_db**  を実行します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または >0 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 db_owner のアクセス許可が必要です。  
  
## <a name="remarks"></a>コメント  
 **Sp_rda_deauthorize_db** を実行すると、Stretch が有効なデータベースとテーブルに対するすべてのクエリが失敗します。 つまり、クエリモードは [無効] に設定されます。 このモードを終了するには、次のいずれかの操作を行います。  
  
-   [Sys.sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)を実行して、リモートの Azure データベースに再接続します。 この操作により、クエリモードが自動的に LOCAL_AND_REMOTE にリセットされます。これは Stretch Database の既定の動作です。 つまり、クエリはローカルとリモートの両方のデータから結果を返します。  
  
-   クエリをローカルデータに対してのみ実行できるようにするには、LOCAL_ONLY 引数を使用して [transact-sql&#41;を sys.sp_rda_set_query_mode &#40;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 実行します。  
  
## <a name="see-also"></a>参照  
 [sys.sp_rda_set_query_mode &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys.sp_rda_reauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
