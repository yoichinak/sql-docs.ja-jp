---
description: sys.dm_os_stacks (Transact-SQL)
title: sys.dm_os_stacks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
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
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 27cc4ae0dd6629ab1801d79a19a1212b4e325ba6
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100344301"
---
# <a name="sysdm_os_stacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  この動的管理ビューは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、次の操作を実行するためにによって内部的に使用されます。  
  
-   未処理の割り当てなど、デバッグデータを追跡します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コンポーネントが特定の呼び出しが行われたと想定している場所のコンポーネントによって使用されるロジックを想定または検証します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary (8)**|このスタック割り当ての一意のアドレス。 NULL 値は許可されません。|  
|**frame_index**|**int**|各行は、特定の **stack_address** に対してフレームインデックスによって昇順に並べ替えられた場合に、完全な呼び出し履歴を返す関数呼び出しを表します。 NULL 値は許可されません。|  
|**frame_address**|**varbinary (8)**|関数呼び出しのアドレス。 NULL 値は許可されません。|  
  
## <a name="remarks"></a>解説  
 **sys.dm_os_stacks** には、サーバーとその他のコンポーネントのシンボルが、情報を正しく表示するためにサーバー上に存在している必要があります。  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
SQL Database Basic、S0、S1 のサービス目標、およびエラスティックプール内のデータベースについては、 [サーバー管理者](https://docs.microsoft.com/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) アカウントまたは [Azure Active Directory 管理者](https://docs.microsoft.com/azure/azure-sql/database/authentication-aad-overview#administrator-structure) アカウントが必要です。 その他のすべての SQL Database サービスの目的で `VIEW DATABASE STATE` は、データベースで権限が必要になります。   


## <a name="see-also"></a>参照  
  [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
