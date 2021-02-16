---
description: catalog.create_environment_reference (SSISDB データベース)
title: catalog.create_environment_reference (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 48069bea-31cb-4a0e-9849-a07edc94088f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7c7c513bf3fcd720418be0eb79a99f75194d0fb1
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100346831"
---
# <a name="catalogcreate_environment_reference-ssisdb-database"></a>catalog.create_environment_reference (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロジェクトに環境参照を作成します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.create_environment_reference [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @environment_name = ] environment_name  
     , [ @reference_type = ] reference_type  
  [  , [ @environment_folder_name = ] environment_folder_name ]  
  [  , [ @reference_id = ] reference_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
 [ @folder_name = ] *folder_name*  
 環境を参照しているプロジェクトのフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [ @project_name = ] *project_name*  
 環境を参照しているプロジェクトの名前。 *project_name* は **nvarchar(128)** です。  
  
 [ @environment_name = ] *environment_name*  
 参照されている環境の名前。 *Environment_name* は **nvarchar(128)** です。  
  
 [ @reference_type = ] *reference_type*  
 環境をプロジェクトと同じフォルダーに配置できるか (相対参照)、または別のフォルダーに配置できるか (絶対参照) を示します。 相対参照を指定するには、値 `R` を使用します。 絶対参照を指定するには、値 `A` を使用します。 *reference_type* は **char(1)** です。  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 参照先の環境があるフォルダーの名前。 この値は絶対参照にする必要があります。 *environment_folder_name* は **nvarchar(128)** です。  
  
 [ @reference_id = ] *reference_id*  
 新しい参照の一意識別子を返します。 このパラメーターは省略可能です。 *reference_id* は **bigint** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトに対する READ および MODIFY 権限、および環境に対する READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   フォルダー名が無効  
  
-   プロジェクト名が無効  
  
-   ユーザーに適切な権限がない  
  
-   *reference_location* パラメーターの `A` 文字を使用して絶対参照が指定されているが、フォルダー名は *environment_folder_name* パラメーターで指定されなかった。  
  
## <a name="remarks"></a>解説  
 プロジェクトでは、相対または絶対環境参照を使用できます。 相対参照は、名前によって環境を参照し、プロジェクトと同じフォルダーに格納されている必要があります。 絶対参照の場合、名前とフォルダーによって環境を参照します。プロジェクトとは異なるフォルダーに格納されている環境を参照する場合があります。 プロジェクトでは複数の環境を参照できます。  
  
  
