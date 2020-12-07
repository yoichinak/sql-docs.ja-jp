---
description: sys.sysサーバー (Transact-sql)
title: sys.sysサーバー (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysservers
- sysservers_TSQL
- sysservers
- sys.sysservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysservers system table
- sys.sysservers compatibility view
ms.assetid: d02f186f-c00f-44a6-b38d-dc78a3d2145b
author: rothja
ms.author: jroth
ms.openlocfilehash: ea79d90f7ccb75243246cc64713c746e05c8996c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475128"
---
# <a name="syssysservers-transact-sql"></a>sys.sysサーバー (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが OLE DB データ ソースとしてアクセスできるサーバーごとに、1 行のデータを格納します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|リモートサーバーの ID (ローカルでのみ使用)。|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|サーバーの名前。|  
|**srvproduct**|**sysname**|リモート サーバーの製品名。|  
|**プロバイダー**|**nvarchar(128)**|サーバーへのアクセスを提供する OLE DB プロバイダー名。|  
|**ソース**|**nvarchar (4000)**|データソース値を OLE DB します。|  
|**location**|**nvarchar (4000)**|OLE DB の場所の値です。|  
|**providerstring**|**nvarchar (4000)**|OLE DB プロバイダーの文字列値。|  
|**schemadate**|**datetime**|この行が最後に更新された日付。|  
|**topologyx**|**int**|使用しません。|  
|**topologyy**|**int**|使用しません。|  
|**catalog**|**sysname**|OLE DB プロバイダーへの接続が確立されるときに使用されるカタログ。|  
|**srvcollation**|**sysname**|サーバーの照合順序。|  
|**connecttimeout**|**int**|サーバー接続のタイムアウト設定です。|  
|**querytimeout**|**int**|サーバーに対するクエリのタイムアウト設定です。|  
|**srvnetname**|**char(30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = サーバーはリモートサーバーです。<br /><br /> 0 = サーバーはリンクサーバーです。|  
|**rpc-epmap**|**bit**|1 = ** \@ rpc** が **true** または on に設定され **て**sp_serveroption。<br /><br /> 0 = **sp_serveroption \@ rpc** が **false** または **off**に設定されています。|  
|**pub**|**bit**|1 = **sp_serveroption \@ pub** が **true** または **on**に設定されています。<br /><br /> 0 = **sp_serveroption \@ pub** が **false** または **off**に設定されています。|  
|**sub**|**bit**|1 = **sp_serveroption \@ sub** が **true** または **on**に設定されています。<br /><br /> 0 = **sp_serveroption \@ sub** を **false** または **off**に設定します。|  
|**dist**|**bit**|1 = **sp_serveroption \@ dist** が **true** または **on**に設定されています。<br /><br /> 0 = **sp_serveroption \@ dist** が **false** または **off**に設定されています。|  
|**dpub**|**bit**|1 = **sp_serveroption \@ dpub** が **true** または **on**に設定されています。<br /><br /> 0 = **sp_serveroption \@ dpub** が **false** または **off**に設定されています。|  
|**rpcout**|**bit**|1 = **sp_serveroption \@ rpc out** が **true** または **on**に設定されています。<br /><br /> 0 = **sp_serveroption \@ rpc out** が **false** または **off**に設定されています。|  
|**dataaccess**|**bit**|1 = **sp_serveroption \@ データアクセス** が **true** または **on**に設定されています。<br /><br /> 0 = **sp_serveroption \@ データアクセス** が **false** または **off**に設定されています。|  
|**collationcompatible**|**bit**|1 = **sp_serveroption \@ 照合順序互換** に設定 **true** または **on**です。<br /><br /> 0 = **sp_serveroption \@ 照合順序互換** に設定 **false** または **オフ**です。|  
|**システム**|**bit**|1 = **sp_serveroption \@ システム** が **true** または **on**に設定されています。<br /><br /> 0 = **sp_serveroption \@ システム** が **false** または **off**に設定されています。|  
|**useremotecollation**|**bit**|1 = ** \@ リモート照合順序** が **true** または **on**に設定されて sp_serveroption。<br /><br /> 0 = ** \@ リモート照合順序** を **false** または **off**に設定 sp_serveroption ます。|  
|**lazyschemavalidation**|**bit**|1 = **sp_serveroption \@ lazy schema validation** を **true** または **on**に設定します。<br /><br /> 0 = **sp_serveroption \@ lazy schema validation** を **false** または **off**に設定します。|  
|**規則**|**sysname**|**Sp_serveroption の \@ 照合順序名**によって設定されたサーバーの照合順序。|  
|**nonsqlsub**|bit|0 = サーバーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス。<br /><br /> 1 = サーバーはのインスタンスではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>参照  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
