---
description: sys.dm_os_stacks (Transact-SQL)
title: dm_os_stacks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_stacks
- dm_os_stacks_TSQL
- sys.dm_os_stacks
- sys.dm_os_stacks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_stacks dynamic management view
ms.assetid: a69b06c4-28f0-4535-8fa1-9f132db4d916
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83b694a70145637dce66e33ea417d1afc660af8e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542130"
---
# <a name="sysdm_os_stacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  この動的管理ビューは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、次の操作を実行するためにによって内部的に使用されます。  
  
-   未処理の割り当てなど、デバッグデータを追跡します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コンポーネントが特定の呼び出しが行われたと想定している場所のコンポーネントによって使用されるロジックを想定または検証します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary (8)**|このスタック割り当ての一意のアドレス。 NULL 値は許可されません。|  
|**frame_index**|**int**|各行は、特定の **stack_address**に対してフレームインデックスによって昇順に並べ替えられた場合に、完全な呼び出し履歴を返す関数呼び出しを表します。 NULL 値は許可されません。|  
|**frame_address**|**varbinary (8)**|関数呼び出しのアドレス。 NULL 値は許可されません。|  
  
## <a name="remarks"></a>解説  
 **dm_os_stacks** には、サーバーとその他のコンポーネントのシンボルが、情報を正しく表示するためにサーバー上に存在している必要があります。  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   


## <a name="see-also"></a>参照  
  [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
