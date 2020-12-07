---
description: catalog.create_folder (SSISDB データベース)
title: catalog.create_folder (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9c0c28c81f607f5ab7ddc71d84ae52ea848d9334
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129862"
---
# <a name="catalogcreate_folder-ssisdb-database"></a>catalog.create_folder (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーを作成します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.create_folder [ @folder_name = ] folder_name, [ @folder_id = ] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
 [@folder_name =] *folder_name*  
 新しいフォルダーの名前です。 *folder_name* は **nvarchar(128)** です。  
  
 [@folder_name =] *folder_id*  
 フォルダーの一意識別子 (ID)。 *folder_id* は **bigint** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 フォルダーの識別子が返されます。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
同じ名前のフォルダーが既に存在する場合、ストアド プロシージャはエラーを返します。  
  
  
