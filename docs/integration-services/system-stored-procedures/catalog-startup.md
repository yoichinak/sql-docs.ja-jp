---
description: catalog.startup
title: catalog.startup |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d3ad08806328cbeb1e99ff997db9dc6593ce9430
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129604"
---
# <a name="catalogstartup"></a>catalog.startup 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SSISDB カタログに対する操作の状態のメンテナンスを実行します。  
  
 このストアド プロシージャは、[!INCLUDE[ssIS](../../includes/ssis-md.md)] サーバー インスタンスがダウンした場合に、実行されていたパッケージの状態を修正します。  
  
 **[カタログの作成]** ダイアログ ボックスの **[Enable automatic execution of Integration Services stored procedure at SQL Server startup]\(SQL Server の起動時に Integration Services ストアド プロシージャの自動実行を有効にする\)** オプションを選択すると、[!INCLUDE[ssIS](../../includes/ssis-md.md)] インスタンスが再起動されるたびに、ストアド プロシージャが自動実行されるようにできます。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.startup  
```  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ および MODIFY 権限、プロジェクトの READ および EXECUTE 権限、参照先の環境の READ 権限 (該当する場合)。  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
  
