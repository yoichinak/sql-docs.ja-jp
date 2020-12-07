---
description: catalog.add_execution_worker (SSISDB データベース)
title: catalog.add_execution_worker (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
author: chugugrace
ms.author: chugu
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 102277139885379f4c2f75c912756e09131ec546
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129950"
---
# <a name="catalogadd_execution_worker-ssisdb-database"></a>catalog.add_execution_worker (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker を Scale Out 内の実行のインスタンスに追加します。

## <a name="syntax"></a>構文

```sql
catalog.add_execution_worker [ @execution_id = ] execution_id, [ @workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>引数
[ @execution_id = ] *execution_id*  
 実行のインスタンスの一意の識別子。 *execution_id* は **bigint** です。  
 
[@workeragent_id = ] *workeragent_id*  
Scale Out Worker の worker エージェント ID。 *workeragent_id* は **uniqueIdentifier** です。

## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  

## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ および MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
 
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
 
- ユーザーに適切なアクセス許可がない。

- 実行識別子が有効ではない。

- worker エージェント ID が正しくない。

- Scale Out に実行がない。

## <a name="see-also"></a>関連項目
[Scale Out でのパッケージの実行](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)。

