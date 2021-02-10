---
title: sys.fn_PageResCracker (Transact-sql) |Microsoft Docs
description: Sys.fn_PageResCracker システム関数について説明します。 サンプルを参照し、使用可能なその他のリソースを確認します。
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- fn_PageResCracker
- sys.fn_PageResCracker_TSQL
- fn_PageResCracker_TSQL
- sys.fn_PageResCracker
- sys.dm_db_page_info
dev_langs:
- TSQL
helpviewer_keywords:
- fn_PageResCracker function
- page_resource
- sys.fn_PageResCracker function
- sys.dm_db_page_info
- page info
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: 49e8472353f19bcca00e68969579d4cbf6f0b538
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100064827"
---
# <a name="sysfn_pagerescracker-transact-sql"></a>sys.fn_PageResCracker (Transact-sql)
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

`db_id`指定された値の、、およびを返し `file_id` `page_id` `page_resource` ます。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>引数  
*page_resource*    
データベースページリソースの8バイトの16進形式です。
  
## <a name="tables-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|db_id|**int**|データベース ID|  
|file_id|**int**|ファイル ID|  
|page_id|**int**|ページ ID|  
  
## <a name="remarks"></a>解説  
`sys.fn_PageResCracker` は、データベースページの8バイトの16進数表現を、ページのデータベース ID、ファイル ID、およびページ ID を含む行セットに変換するために使用されます。   

有効なページリソースを取得するには、 `page_resource` sys.dm_exec_requests の列から [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 動的管理ビュー、または [sys.sys](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) の &#40;システムビュー&#41;ます。 無効なページリソースが使用されている場合、戻り値は NULL になります。  
の主な用途 `sys.fn_PageResCracker` は、これらのビューと [Sys.dm_db_page_info &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) 動的管理関数との間の結合を容易にすることです。これにより、そのページが属するオブジェクトなどのページに関する情報を取得できます。
  
## <a name="permissions"></a>アクセス許可  
ユーザーは、 `VIEW SERVER STATE` サーバーに対する権限が必要です。  
  
## <a name="examples"></a>例  
`sys.fn_PageResCracker`関数を[Sys.dm_db_page_info &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)と組み合わせて使用して、でのページ関連の待機およびブロックのトラブルシューティングを行うことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  次のスクリプトは、特定の種類のページリソースで現在待機しているすべてのアクティブな要求について、データベースページ情報を収集するためにこれらの関数を使用する方法の例です。 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>参照  
 [sys.dm_db_page_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sys.sysプロセス &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
