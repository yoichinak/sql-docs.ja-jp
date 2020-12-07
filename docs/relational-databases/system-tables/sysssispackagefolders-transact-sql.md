---
description: sysssispackagefolders (Transact-sql)
title: sysssispackagefolders (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7924de782ca499f5a92458d0024b57877c7310c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419126"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  が使用するフォルダー階層内の論理フォルダーごとに1行のレコードを格納 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] します。 これらのフォルダーは、に接続するときにオブジェクトエクスプローラーの一覧に表示され [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ます。 フォルダーには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはファイル システムに保存されているパッケージが一覧表示されます。  
  
 **Parentfolderid**列には、フォルダー階層が記述されています。 フォルダー階層の最上位にあるフォルダーには、 **parentfolderid**に null 値が含まれています。  
  
 **Foldername**列にはオブジェクトエクスプローラーに表示されるフォルダーの名前が含まれています。  
  
 このテーブルは、 **msdb** データベースに格納されます。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|フォルダーの GUID。|  
|**parentfolderid**|**uniqueidentifier**|親フォルダーであるフォルダーの GUID。|  
|**名**|**sysname**|フォルダーの名前。 これは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でフォルダー階層に表示される名前です。|  
  
  
