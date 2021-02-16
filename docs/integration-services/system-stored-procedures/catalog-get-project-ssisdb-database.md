---
description: catalog.get_project (SSISDB データベース)
title: catalog.get_project (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a39f9b085c5d37a16207760a83064ede4cedb290
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100342222"
---
# <a name="catalogget_project-ssisdb-database"></a>catalog.get_project (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置されたプロジェクトのバイナリ ストリームを取得します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>引数  
 [ @folder_name = ] *folder_name*  
 プロジェクトを含むフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [ @project_name = ] *project_name*  
 プロジェクトの名前です。 *project_name* は **nvarchar(128)** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 プロジェクトのバイナリ ストリームは **varbinary(MAX)** として返されます。 フォルダーまたはプロジェクトが見つからない場合、結果は返されません。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトに対する READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 次の一覧は、get_project ストアド プロシージャにエラーを発生させる可能性があるいくつかの条件を以下に示します。  
  
-   プロジェクトが存在しない  
  
-   フォルダーが存在しない  
  
-   ユーザーに適切な権限がない  
  
  
