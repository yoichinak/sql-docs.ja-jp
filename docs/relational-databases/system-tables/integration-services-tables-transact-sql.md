---
description: Integration Services テーブル (Transact-sql)
title: Integration Services テーブル (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 05f7e319dbaec37761eb5488f9d9a33cce09f3a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473251"
---
# <a name="integration-services-tables-transact-sql"></a>Integration Services テーブル (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このセクションのトピックでは、によって使用される情報を格納する msdb データベース内のシステムテーブルについて説明し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 パッケージが実行時に生成するログエントリごとに1行のレコードを格納 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] します。  
  
 このテーブルは、パッケージで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログ プロバイダーが使用されている場合にのみ使用されます。  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]サービスがパッケージを整理するために使用する論理フォルダーごとに1行の値を格納します。 列の値は、入れ子になったフォルダー間の親子関係を定義します。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] サービスに接続した場合、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の階層ビューに、格納されているパッケージが表示されます。  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 パッケージごとに1行の値を格納 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] します。  
  
 このテーブルは、でパッケージを格納する場合にのみ使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
  
