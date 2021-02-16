---
description: catalog.move_project (SSISDB データベース)
title: catalog.move_project (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ef3b0325-d8e9-472b-bf11-7d3efa6312ff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4c7cf1e3c23eacbabfd59ba3b8948740dc1a0543
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100342190"
---
# <a name="catalogmove_project---ssisdb-database"></a>catalog.move_project - SSISDB データベース

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  特定のフォルダーのプロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログ内の別のフォルダーに移動します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.move_project [ @source_folder = ] source_folder  
    , [ @project_name = ] project_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>引数  
 [ @source_folder = ] *source_folder*  
 プロジェクトが、移動前に配置されていたソース フォルダーの名前。 *source_folder* は **nvarchar(128)** です。  
  
 [ @project_name = ] *project_name*  
 移動されるプロジェクトの名前。 *project_name* は **nvarchar(128)** です。  
  
 [ @destination_folder = ] *destination_folder*  
 プロジェクトが移動後に配置される移動先フォルダーの名前。 *destination_folder* は **nvarchar(128)** です。  
  
## <a name="return-code-value"></a>リターン コード値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   移動するプロジェクトに対する READ および MODIFY 権限と、移動先フォルダーに対する CREATE_OBJECTS 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 このストアド プロシージャがエラーを発生させる可能性がある条件を以下に示します。  
  
-   プロジェクトが存在しない  
  
-   移動元フォルダーが存在しない  
  
-   移動先フォルダーが存在しないか、移動先フォルダーに同じ名前のプロジェクトが既にある  
  
-   ユーザーに適切な権限がない  
  
## <a name="remarks"></a>注釈  
 プロジェクトを元のフォルダーから目的のフォルダーに移動すると、ソース フォルダーのプロジェクトと、対応する環境参照が削除されます 移動先のフォルダーには、同じプロジェクトと環境参照が作成されます。 相対環境参照は、移動後、別のフォルダーに解決されます。 絶対参照は、移動後、同じフォルダーに解決されます。  
  
> [!NOTE]  
>  プロジェクトでは、相対または絶対環境参照を使用できます。 相対参照の場合、名前によって環境を参照します。この環境はプロジェクトと同じフォルダーに格納されている必要があります。 絶対参照の場合、名前とフォルダーによって環境を参照します。これらの参照は、プロジェクトとは異なるフォルダーに格納されている環境を参照する場合があります。  
  
  
