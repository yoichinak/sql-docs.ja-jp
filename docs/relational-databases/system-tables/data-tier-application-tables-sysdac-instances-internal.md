---
description: データ層アプリケーション テーブル - sysdac_instances_internal
title: sysdac_instances_internal (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_instances_internal_TSQL
- sysdac_instances_internal
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_instances_internal
ms.assetid: d2d52cc4-3463-431a-b779-6fbfdeee1dfc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ccda567989211074c8d151de7f2b3936ccd2b69
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544612"
---
# <a name="data-tier-application-tables---sysdac_instances_internal"></a>データ層アプリケーション テーブル - sysdac_instances_internal
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに配置されたデータ層アプリケーション (DAC) インスタンスごとに 1 行を表示します。 このテーブルは、msdb データベースの dbo スキーマに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|DAC インスタンスの識別子。|  
|instance_name|**sysname**|インスタンスの配置時に指定された DAC インスタンスの名前。|  
|type_name|**sysname**|DAC パッケージの作成時に指定された DAC の名前。|  
|type_version|**nvarchar (64)**|DAC パッケージの作成時に指定された DAC のバージョン。|  
|description|**nvarchar (4000)**|DAC パッケージの作成時に指定された DAC の説明。|  
|type_stream|**varbinary(max)**|DAC に含まれるテーブルやビューなどの論理オブジェクトのエンコードされた表現を格納しているビットストリーム。|  
|date_created|**datetime**|DAC インスタンスが作成された日付と時刻。|  
|created_by|**sysname**|DAC インスタンスを作成したログイン。|  
  
## <a name="remarks"></a>解説  
 このビューへの読み取り専用アクセスは、master データベースに接続する権限を持つすべてのユーザーが使用できます。  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)  
  
  
