---
description: dm_clr_loaded_assemblies (Transact-sql)
title: dm_clr_loaded_assemblies (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_loaded_assemblies
- sys.dm_clr_loaded_assemblies_TSQL
- dm_clr_loaded_assemblies_TSQL
- sys.dm_clr_loaded_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_loaded_assemblies dynamic management view
ms.assetid: 8523d8db-d8a0-4b1f-ae19-6705d633e0a6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 42abc84bf1b5a78979da4c7443158abc6eddabc8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539462"
---
# <a name="sysdm_clr_loaded_assemblies-transact-sql"></a>dm_clr_loaded_assemblies (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーのアドレス空間に読み込まれた管理対象ユーザーアセンブリごとに1行の値を返します。 このビューを使用すると、で実行されている CLR 統合マネージデータベースオブジェクトについて理解し、トラブルシューティングを行うことが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] できます。  
  
 アセンブリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド データベース オブジェクトの定義や配置のために使用されるマネージド コード DLL ファイルです。 ユーザーがこれらのマネージデータベースオブジェクトのいずれかを実行するたびに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージデータベースオブジェクトが定義されているアセンブリ (およびその参照) が CLR によって読み込まれます。 アセンブリは、パフォーマンス向上のために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込まれたままになるので、その後は、アセンブリを再度読み込まなくても、アセンブリに含まれているマネージド データベース オブジェクトを呼び出すことができます。 がメモリ不足になるまで、アセンブリはアンロードされません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 アセンブリと CLR 統合の詳細については、「 [Clr ホステッド環境](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)」を参照してください。 マネージデータベースオブジェクトの詳細については、「 [CLR&#41; 統合 &#40;共通言語ランタイムを使用したデータベースオブジェクトの構築](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)」を参照してください。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|読み込まれたアセンブリの ID。 **Assembly_id**を使用すると、 [transact-sql&#41;](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)カタログビュー &#40;のアセンブリに関する詳細情報を参照できます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)現在のデータベースのみにアセンブリが表示されていることに注意してください。 Dm_clr_loaded_assemblies ビューには、サーバー上のすべての読み込ま **れ** たアセンブリが表示されます。|  
|**appdomain_address**|**int**|アセンブリが読み込まれるアプリケーションドメイン (**AppDomain**) のアドレス。 1人のユーザーが所有するすべてのアセンブリは、常に同じ **AppDomain**に読み込まれます。 **Appdomain_address**を使用すると、 [Dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)ビューで**appdomain**に関する詳細情報を参照できます。|  
|**load_time**|**datetime**|アセンブリが読み込まれた時刻。 がメモリ不足になるまでアセンブリが読み込まれ、AppDomain がアンロードされることに注意して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ください。 **AppDomain** **Load_time**を監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] して、メモリ不足の発生頻度を把握し、 **AppDomain**をアンロードできます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="remarks"></a>解説  
 Appdomain_address ビューには **dm_clr_loaded_assemblies** 、  **dm_clr_appdomains appdomain_address**との多対一のリレーションシップがあります。 **Dm_clr_loaded_assemblies assembly_id**ビューには、 **assembly_id**との一対多のリレーションシップがあります。  
  
## <a name="examples"></a>例  
 次の例は、現在読み込まれている現在のデータベースのすべてのアセンブリの詳細を表示する方法を示しています。  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 次の例は、特定のアセンブリが読み込まれる **AppDomain** の詳細を表示する方法を示しています。  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;共通言語ランタイム関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
