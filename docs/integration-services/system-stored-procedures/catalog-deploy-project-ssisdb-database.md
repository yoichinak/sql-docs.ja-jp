---
description: catalog.deploy_project (SSISDB データベース)
title: catalog.deploy_project (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6a8bb809f349ce68b12abaee171928805d1fe0df
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129809"
---
# <a name="catalogdeploy_project-ssisdb-database"></a>catalog.deploy_project (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーにプロジェクトを配置するか、以前に配置した既存のプロジェクトを更新します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.deploy_project [@folder_name =] folder_name   
      , [ @project_name = ] project_name   
      , [ @project_stream = ] projectstream   
    [ , [ @operation_id = ] operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>引数  
 [@folder_name =] *folder_name*  
 プロジェクトが配置されるフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [@project_name =] *project_name*  
 フォルダー内の新規または更新されたプロジェクトの名前。 *project_name* は **nvarchar(128)** です。  
  
 [@projectstream =] *projectstream*  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクト配置ファイル (拡張子は .ispac) のバイナリ コンテンツ。  
  
 ファイルのバイナリ コンテンツを取得するには、SELECT ステートメントと、OPENROWSET 関数および一括行セット プロバイダーを使用できます。 例については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。 OPENROWSET の詳細については、「[OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)」を参照してください。  
  
 *projectstream* は **varbinary(max)**  
  
 [@operation_id =] *operation_id*  
 配置操作の一意識別子を返します。 *operation_id* は **bigint** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   新しいプロジェクトを配置するフォルダーに対する CREATE_OBJECTS 権限、またはプロジェクトを更新するプロジェクトに対する MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 このストアド プロシージャがエラーを発生させる可能性がある条件を以下に示します。  
  
-   存在しないオブジェクトを参照するパラメーター、既に存在するオブジェクトを作成しようとするパラメーター、または何かの方法で無効になるパラメーター  
  
-   パラメーター *\@project_name* の値が、配置ファイルのプロジェクトの名前に一致しない  
  
-   ユーザーに十分な権限がない  
  
## <a name="remarks"></a>注釈  
 プロジェクトの配置または更新中、ストアド プロシージャは、プロジェクトの個々のパッケージの保護レベルをチェックしません。  
  
  
