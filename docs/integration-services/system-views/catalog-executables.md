---
description: catalog.executables
title: catalog.executables | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3aff9256e3f8468642177a24975489ebf7ebd646
ms.sourcegitcommit: 868c60aa3a76569faedd9b53187e6b3be4997cc9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99835328"
---
# <a name="catalogexecutables"></a>catalog.executables 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  このビューは、指定した実行の各実行可能ファイルの行を表示します。  
  
 実行可能ファイルは、パッケージの制御フローに追加するタスクまたはコンテナーです。  
  
|列名|**データの種類**|説明|  
|-----------------|-------------------|-----------------|  
|executable_id|**bigint**|実行可能ファイルの一意の識別子。|  
|execution_id|**bigint**|実行のインスタンスの一意の識別子。|  
|executable_name|**nvarchar (4000)**|実行可能ファイルの名前。|  
|executable_guid|**nvarchar(38)**|実行可能ファイルの GUID。|  
|package_name|**nvarchar(260)**|パッケージの名前です。|  
|package_path|**nvarchar(max)**|パッケージのパス。|  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
## <a name="remarks"></a>解説  
  
