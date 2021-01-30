---
title: sys.sp_rda_set_query_mode (Transact-sql) |Microsoft Docs
description: Sys.sp_rda_set_query_mode を使用して、現在の Stretch が有効なデータベースに対するクエリとそのテーブルがローカルデータとリモートデータのどちらを返すか、またはローカルデータのみを返すかを指定します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ed9e5afda379b094a61c9f6d3130b986e0b83ca3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99211724"
---
# <a name="syssp_rda_set_query_mode-transact-sql"></a>sys.sp_rda_set_query_mode (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  現在の Stretch が有効なデータベースとそのテーブルに対するクエリがローカルデータとリモートデータの両方を返すかどうかを指定します (既定)。またはローカルデータのみを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>引数  
 [ @mode =] *\@ モード*  
 次のいずれかの値を指定します。  
  
-   **無効** Stretch が有効なテーブルに対するすべてのクエリが失敗します。  
  
-   **LOCAL_ONLY** Stretch が有効なテーブルに対するクエリでは、ローカルデータのみが返されます。  
  
-   **LOCAL_AND_REMOTE** Stretch が有効なテーブルに対するクエリでは、ローカルデータとリモートデータの両方が返されます。 これが既定の動作です。  
  
 [ @force =] *\@ force*  
 検証せずにクエリモードを変更する場合は、1に設定できるビット値を指定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または >0 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 db_owner のアクセス許可が必要です。  
  
## <a name="remarks"></a>コメント  
 次の拡張ストアドプロシージャは、Stretch 対応データベースのクエリモードも設定します。  
  
-   **sp_rda_deauthorize_db**  
  
     **Sp_rda_deauthorize_db** を実行すると、Stretch が有効なデータベースとテーブルに対するすべてのクエリが失敗します。 つまり、クエリモードは [無効] に設定されます。 このモードを終了するには、次のいずれかの操作を行います。  
  
    -   [Sys.sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)を実行して、リモートの Azure データベースに再接続します。 この操作により、クエリモードが自動的に LOCAL_AND_REMOTE にリセットされます。これは Stretch Database の既定の動作です。 つまり、クエリはローカルとリモートの両方のデータから結果を返します。  
  
    -   クエリがローカルデータに対してのみ実行されるようにするには、LOCAL_ONLY 引数を指定して [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) を実行します。  
  
-   **sp_rda_reauthorize_db**  
  
     [Sys.sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)を実行してリモートの Azure データベースに再接続すると、この操作によってクエリモードが自動的に LOCAL_AND_REMOTE にリセットされます。これは Stretch Database の既定の動作です。 つまり、クエリはローカルとリモートの両方のデータから結果を返します。  
  
## <a name="see-also"></a>参照  
 [sys.sp_rda_deauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
