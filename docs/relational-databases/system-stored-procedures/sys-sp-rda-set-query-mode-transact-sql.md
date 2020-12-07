---
title: sp_rda_set_query_mode (Transact-sql) |Microsoft Docs
description: 現在の Stretch が有効なデータベースに対するクエリが、ローカルデータとリモートデータ、またはローカルデータのみを返すかどうかを指定するには、sp_rda_set_query_mode を使用します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
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
ms.openlocfilehash: 26b8a363de2faf9e39bc88e3dd1e0a26bd016e16
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540452"
---
# <a name="syssp_rda_set_query_mode-transact-sql"></a>sp_rda_set_query_mode (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  現在の Stretch が有効なデータベースとそのテーブルに対するクエリがローカルデータとリモートデータの両方を返すかどうかを指定します (既定)。またはローカルデータのみを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>引数  
 [ @mode =] * \@ モード*  
 次のいずれかの値を指定します。  
  
-   **無効** Stretch が有効なテーブルに対するすべてのクエリが失敗します。  
  
-   **LOCAL_ONLY** Stretch が有効なテーブルに対するクエリでは、ローカルデータのみが返されます。  
  
-   **LOCAL_AND_REMOTE** Stretch が有効なテーブルに対するクエリでは、ローカルデータとリモートデータの両方が返されます。 これは既定の動作です。  
  
 [ @force =] * \@ force*  
 検証せずにクエリモードを変更する場合は、1に設定できるビット値を指定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または >0 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 Db_owner のアクセス許可が必要です。  
  
## <a name="remarks"></a>解説  
 次の拡張ストアドプロシージャは、Stretch 対応データベースのクエリモードも設定します。  
  
-   **sp_rda_deauthorize_db**  
  
     **Sp_rda_deauthorize_db**を実行すると、Stretch が有効なデータベースとテーブルに対するすべてのクエリが失敗します。 つまり、クエリモードは [無効] に設定されます。 このモードを終了するには、次のいずれかの操作を行います。  
  
    -   [Transact-sql&#41;&#40;sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)を実行して、リモートの Azure データベースに再接続します。 この操作により、クエリモードが自動的に LOCAL_AND_REMOTE にリセットされます。これは Stretch Database の既定の動作です。 つまり、クエリはローカルとリモートの両方のデータから結果を返します。  
  
    -   ローカルデータに対してのみクエリを実行できるようにするには、LOCAL_ONLY 引数を指定して sp_rda_set_query_mode を実行し [ます](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 。  
  
-   **sp_rda_reauthorize_db**  
  
     [Sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)を実行してリモートの Azure データベースに再接続すると、この操作によってクエリモードが自動的に LOCAL_AND_REMOTE にリセットされます。これは Stretch Database の既定の動作です。 つまり、クエリはローカルとリモートの両方のデータから結果を返します。  
  
## <a name="see-also"></a>参照  
 [sp_rda_deauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
