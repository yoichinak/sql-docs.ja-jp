---
description: catalog.master_properties (SSISDB データベース)
title: catalog.master_properties (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09e13f54b3e7ee92ed72b055246ea1235845448f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422056"
---
# <a name="catalogmaster_properties-ssisdb-database"></a>catalog.master_properties (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master のプロパティを表示します。

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar (256)**|Scale Out Master のプロパティの名前。|  
|property_value|**nvarchar(max)**|Scale Out Master のプロパティの値。|

## <a name="remarks"></a>解説
このビューは、各 Scale Out Master のプロパティの行を表示します。 このビューで表示されるプロパティは、次のとおりです。

|プロパティ名|説明|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|ログ データベースのある SQL Server。|
|**LAST_ONLINE_TIME**|Scale Out Master がオンラインになった最後の時刻。|
|**MACHINE_IP**|コンピューターの IP。|
|**MACHINE_NAME**|コンピューターの名前です。|
|**MASTER_ADDRESS**|Scale Out Master のエンドポイント。|
|**MASTER_SERVICE_PORT**|Scale Out Master のエンドポイントのポート。|
|**SSLCERT_THUMBPRINT**|Scale Out Master 証明書の拇印。|

## <a name="permissions"></a>アクセス許可
public データベース ロールのすべてのメンバーにこのビューの読み取りアクセス許可が与えられます。 
