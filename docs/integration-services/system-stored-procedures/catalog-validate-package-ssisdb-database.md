---
description: catalog.validate_package (SSISDB データベース)
title: catalog.validate_package (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- validate_package stored procedure [Integration Services]
- catalog.validate_package stored procedure [Integration Services]
ms.assetid: 0dc03df1-b793-408f-af4c-c11188729abf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 632a0039692cbb6d22dba736f268bffff9be6f74
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129495"
---
# <a name="catalogvalidate_package-ssisdb-database"></a>catalog.validate_package (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのパッケージを非同期的に検証します。  
  
## <a name="syntax"></a>構文  
  
```sql
catalog.validate_package [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @package_name = ] package_name  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @environment_scope = ] environment_scope ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>引数  
 [ @folder_name = ] *folder_name*  
 パッケージを含むフォルダーの名前。 *folder_name* は **nvarchar(128)** です。  
  
 [ @project_name = ] *project_name*  
 パッケージを含むプロジェクトの名前。 *project_name* は **nvarchar(128)** です。  
  
 [ @package_name = ] *package_name*  
 パッケージの名前です。 *package_name* は **nvarchar (260)** です。  
  
 [ @validation_id = ] *validation_id*  
 検証の一意識別子 (ID) を返します。 *validation_id* は **bigint** です。  
  
 [ @use32bitruntime = ] *use32bitruntime*  
 64 ビット オペレーティング システムで 32 ビットのランタイムを使用してパッケージを実行すべきかどうかを示します。 値 `1` を使用して 64 ビットのオペレーティング システムで実行されているときに、32 ビット ランタイムを使用してパッケージを実行します。 値 `0` を使用すると、64 ビット オペレーティング システムで実行しているときに、64 ビット ランタイムでパッケージが実行されます。 このパラメーターは省略可能です。 *use32bitruntime* は **bit** です。  
  
 [ @environment_scope = ] *environment_scope*  
 検証が考慮する環境参照を示します。 値が `A` の場合は、プロジェクトに関連するすべての環境参照が検証に含まれます。 値が `S` の場合は、1 つの環境参照のみが含まれます。 値が `D` の場合、環境参照は含まれず、各パラメーターには、検証に合格するため、既定のリテラル値を指定する必要があります。 このパラメーターは省略可能です。 文字 `D` が既定で使用されます。 *environment_scope* は **char(1)** です。  
  
 [ @reference_id = ] *reference_id*  
 環境参照の一意の ID。 このパラメーターは、検証に 1 つの環境参照が含まれていて、*environment_scope* が `S` の場合にのみ必要です。 *reference_id* は **bigint** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトの READ 権限と、該当する場合は、参照先の環境での READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 エラーまたは警告が発生する可能性がある条件を以下に示します。  
  
-   プロジェクト名またはパッケージ名が無効  
  
-   ユーザーに適切な権限がない  
  
-   検証に含まれる 1 つまたは複数の参照先の環境が、参照先の変数を含まない  
  
-   パッケージの検証に失敗する  
  
-   参照先の環境が存在しない  
  
-   参照先の変数が、検証に含まれる参照先の環境で見つからない  
  
-   変数がパッケージ パラメーターで参照されるが、参照先の環境が検証に含まれなかった  
  
## <a name="remarks"></a>解説  
 検証では、パッケージが正常に実行されない問題を特定することができます。 検証の状態を監視するには、[catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) または [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) ビューを使用します。  
  
  
