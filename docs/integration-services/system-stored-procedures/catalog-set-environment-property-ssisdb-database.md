---
description: catalog.set_environment_property (SSISDB データベース)
title: catalog.set_environment_property (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a345675b-d32e-4624-96cf-ec656730b114
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba69c12d93b683afa8d11669523153dc6d79d0c6
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129721"
---
# <a name="catalogset_environment_property-ssisdb-database"></a>catalog.set_environment_property (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの環境のプロパティを設定します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.set_environment_property [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>引数  
 [ @folder_name = ] *folder_name*  
 環境を含むフォルダーの名前です。 *folder_name* は **nvarchar(128)** です。  
  
 [ @environment_name = ] *environment_name*  
 環境の名前。 *Environment_name* は **nvarchar(128)** です。  
  
 [ @property_name = ] *property_name*  
 環境プロパティの名前。 *Property_name* は **nvarchar(128)** です。  
  
 [ @property_value = ] *property_value*  
 環境プロパティの値。 *Property_value* は **nvarchar (1024)** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   環境の READ および MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   フォルダー名が無効  
  
-   プロパティ名が無効  
  
-   環境名が無効  
  
## <a name="remarks"></a>解説  
 このリリースで設定できるのは `Description` プロパティだけです。 `Description` プロパティのプロパティ値は 4,000 文字を超えることはできません。  
  
  
