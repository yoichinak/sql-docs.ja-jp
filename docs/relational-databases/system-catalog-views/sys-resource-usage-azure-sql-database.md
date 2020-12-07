---
description: sys.resource_usage (Azure SQL データベース)
title: resource_usage (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_usage_TSQL
- resource_usage
- sys.resource_usage
- resource_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- resource_usage
- sys.resource_usage
ms.assetid: b90147a3-fd8e-408e-961d-5c7000e068ad
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d7f5a7aadb3a16a673bca0d8c0ba34108a158693
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447816"
---
# <a name="sysresource_usage-azure-sql-database"></a>sys.resource_usage (Azure SQL データベース)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

    
> [!IMPORTANT]
>  この機能はプレビュー状態です。 この機能は将来のリリースで変更または削除される可能性があるので、この機能の具体的な実装への依存関係を導入しないでください。  
> 
>  プレビュー状態の間、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] オペレーション チームは、この DMV のデータ収集をオフまたはオンにしている可能性があります。  
> 
>  -   有効になっていると、DMV は集計時点の現在のデータを返します。  
> -   無効になっていると、DMV は古くなった可能性のある履歴データを返します。  
  
 現在のサーバーにおけるユーザー データベースのリソース使用状況データの毎時の集計を返します。 履歴データは90日間保持されます。  
  
 各ユーザー データベースについて、毎時 1 行のデータが連続的に含まれます。 データベースがアイドル状態であった時間に対する行も含まれ、そのデータベースの usage_in_seconds 値は 0 になります。 対象時間のストレージの使用率および SKU 情報が適切にロール アップされます。  
  
|[列]|データ型|説明|  
|-------------|---------------|-----------------|  
|time|**datetime**|1 時間単位の時刻 (UTC) です。|  
|database_name|**nvarchar**|ユーザー データベースの名前です。|  
|sku|**nvarchar**|SKU の名前です。 使用できる値を次に示します。<br /><br /> Web<br /><br /> Business<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|1 時間の間隔において使用された CPU 時間の合計。<br /><br /> 注: この列は V11 では非推奨とされており、V12 には適用されません。 **値は常に0に設定されます。**|  
|storage_in_megabytes|**decimal**|対象時間内のストレージの最大サイズです。データベース データ、インデックス、ストアド プロシージャ、およびメタデータを含みます。|  
  
## <a name="permissions"></a>アクセス許可  
 このビューは、仮想 **master** データベースに接続するためのアクセス許可を持つすべてのユーザーロールで使用できます。  
  
  
