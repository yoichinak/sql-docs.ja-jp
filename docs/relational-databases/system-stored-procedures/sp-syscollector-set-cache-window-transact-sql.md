---
description: sp_syscollector_set_cache_window (Transact-SQL)
title: sp_syscollector_set_cache_window (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_window
- sp_syscollector_set_cache_window_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_set_cache_window stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 660f2749-392f-46bf-89f3-27764d848507
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81d1be542b93a1ceb7bd699e2dbc07a7f3884fa4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541500"
---
# <a name="sp_syscollector_set_cache_window-transact-sql"></a>sp_syscollector_set_cache_window (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  エラーが発生した場合にデータのアップロードを試行する回数を設定します。 データのアップロード時にエラーが発生した場合に再試行することで、収集したデータが失われるリスクが軽減されます。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_set_cache_window [ @cache_window = ] cache_window   
```  
  
## <a name="arguments"></a>引数  
 [ @cache_window =] *cache_window*  
 管理データ ウェアハウスへのデータのアップロード時にエラーが発生した場合、データが失われるのを回避するためにアップロードを再試行する回数を指定します。 *cache_window* は **int** で、既定値は1です。 *cache_window* には、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|-1|アップロード エラーが発生した場合にそのすべてのアップロード データをキャッシュします。|  
|0|アップロードエラーのデータをキャッシュしないでください。|  
|*n*|前回のアップロードエラーのデータをキャッシュします。 *n* >= 1 です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 キャッシュ ウィンドウの構成を変更する前に、データ コレクターを無効にする必要があります。 データ コレクターが有効になっている場合、このストアド プロシージャは失敗します。 詳細については、「 [データコレクションの有効化または無効化](../../relational-databases/data-collection/enable-or-disable-data-collection.md)」と「 [データコレクションの管理](../../relational-databases/data-collection/manage-data-collection.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、dc_admin (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、データコレクターを無効にし、最大3回のアップロードでデータを保持するようにキャッシュウィンドウを構成してから、データコレクターを有効にします。  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXECUTE dbo.sp_syscollector_set_cache_window 3;  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)  
  
  
