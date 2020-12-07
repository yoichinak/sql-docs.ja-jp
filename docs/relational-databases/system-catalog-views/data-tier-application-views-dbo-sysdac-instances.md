---
description: データ層アプリケーションビュー-dbo.sysdac_instances
title: dbo.sysdac_instances (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdac_instances_TSQL
- sysdac_instances
- sysdac_instances_TSQL
- dbo.sysdac_instances
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.sysdac_instances
- sysdac_instances
ms.assetid: 28285f3d-3889-439f-8b24-3bdef08e46b4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1a21fa1559bb09493ae2802254c87235ecc19efc
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809458"
---
# <a name="data-tier-application-views---dbosysdac_instances"></a>データ層アプリケーションビュー-dbo.sysdac_instances
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに配置されたデータ層アプリケーション (DAC) インスタンスごとに 1 行を表示します。 sysdac_instances は、msdb データベースの dbo スキーマに属しています。 次の表では、sysdac_instances ビューの列について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|DAC インスタンスの識別子。|  
|instance_name|**sysname**|DAC の配置時に指定された DAC インスタンスの名前。|  
|type_name|**sysname**|DAC パッケージの作成時に指定された DAC の名前。|  
|type_version|**nvarchar (64)**|DAC パッケージの作成時に指定された DAC のバージョン。|  
|description|**nvarchar (4000)**|DAC パッケージの作成時に指定された DAC の説明。|  
|type_stream|**varbinary(max)**|DAC に含まれるテーブルやビューなどの論理オブジェクトのエンコードされた表現を含むビットストリーム。|  
|date_created|**datetime**|DAC インスタンスが作成された日付と時刻。|  
|created_by|**sysname**|DAC インスタンスを作成したログイン。|  
|database_name|**sysname**|DAC インスタンスのために作成したデータベースの名前。|  
  
## <a name="remarks"></a>注釈  
 DAC には、テーブルやビューなどのアプリケーションによって使用される論理データ層オブジェクトの定義である DAC 型が含まれています。 DAC パッケージは、DAC を配置するために使用されるファイルです。 DAC パッケージは、DAC 型に含まれるすべての論理オブジェクトの表現を含んでいます。 DAC パッケージは、DAC の1つ以上のコピー (インスタンス) をのインスタンスに配置するために使用でき [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。 同じ DAC パッケージから配置された各 DAC インスタンスは同じ種類を共有しますが、一意のインスタンス名と識別子が割り当てられます。  
  
## <a name="permissions"></a>アクセス許可  
 すべての列を表示するには、sysadmin 固定サーバー ロールのメンバーシップが必要です。 パブリック ロールのメンバーは、instance_name、description、および type_version の各列を表示できます。  
  
## <a name="see-also"></a>参照  
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [データ層アプリケーションビュー &#40;Transact-sql&#41;]()  
  
