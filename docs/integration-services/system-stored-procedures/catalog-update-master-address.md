---
description: catalog.update_master_address (SSISDB データベース)
title: catalog.update_master_address (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
author: haoqian
ms.author: haoqian
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 80b5e28a0d552955154849d2f593fc32be79f656
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129528"
---
# <a name="catalogupdate_master_address-ssisdb-database"></a>catalog.update_master_address (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master エンドポイントを更新します。

## <a name="syntax"></a>構文

```sql
catalog.update_master_address [ @MasterAddress = ] masterAddress
```

## <a name="arguments"></a>引数
[ @MasterAddress = ] *masterAddress*  
Scale Out Master エンドポイント。 *masterAddress* は **nvarchar** です。  

 ## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  

## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
   
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
 
