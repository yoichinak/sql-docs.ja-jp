---
description: システム互換性ビュー (Transact-sql)
title: システム互換性ビュー (Transact-sql) |Microsoft Docs
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
- compatibility views [SQL Server]
- system tables [SQL Server], compatibility views
- type IDs [SQL Server]
- system views [SQL Server], compatibility
- metadata [SQL Server], views
- backward compatibility [SQL Server], compatibility views
- compatibility [SQL Server], compatibility views
- backward compatibility [SQL Server], system tables
- compatibility [SQL Server], system tables
- user IDs [SQL Server]
ms.assetid: 8e4624f5-9d36-4ce7-9c9e-1fe010fa2122
author: rothja
ms.author: jroth
ms.openlocfilehash: 3eb92654dfb25a0e66d2e071040e487e6a404366
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482047"
---
# <a name="system-compatibility-views-transact-sql"></a>システム互換性ビュー (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  以前のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の多くのシステム テーブルは、一連のビューとして実装されるようになりました。 これらのビューは互換性ビューと呼ばれ、旧バージョンとの互換性のためだけに用意されています。 互換性ビューでは、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] で利用できるメタデータと同じメタデータを利用できますが、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降で導入された機能に関連するメタデータは利用できません。 したがって、[!INCLUDE[ssSB](../../includes/sssb-md.md)] やパーティションなどの新機能を使用するときは、カタログ ビューを使用するように切り替える必要があります。  
  
 カタログ ビューへアップグレードするもう 1 つの理由としては、ユーザー ID および型 ID を格納する互換性ビューの列では NULL が返されるか算術オーバーフローが発生する可能性があることが挙げられます。 これは、32767を超えるユーザー、グループ、およびロールと32767データ型を作成できるためです。 たとえば、32768ユーザーを作成し、次のクエリを実行したとします `SELECT * FROM sys.sysusers` 。 ここで ARITHABORT が ON に設定されている場合、クエリは算術オーバーフロー エラーで失敗します。 ARITHABORT が OFF に設定されている場合、 **uid** 列は NULL を返します。  
  
 これらの問題を回避するには、増加したユーザー Id と種類 Id を処理できる新しいカタログビューを使用することをお勧めします。 次の表に、このオーバーフローが発生する可能性のある列を示します。  
  
|列名|互換性ビュー|SQL Server 2005 ビュー|  
|-----------------|------------------------|--------------------------|  
|**xusertype**|**syscolumns**|**sys.columns**|  
|**usertype**|**syscolumns**|**sys.columns**|  
|**memberuid**|**sysmembers**|**sys.database_role_members**|  
|**groupuid**|**sysmembers**|**sys.database_role_members**|  
|**uid**|**sysobjects**|**sys.objects**|  
|**uid**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**権限**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**xusertype**|**systypes**|**sys.types**|  
|**uid**|**systypes**|**sys.types**|  
|**uid**|**sysusers**|**sys.database_principals**|  
|**altuid**|**sysusers**|**sys.database_principals**|  
|**gid**|**sysusers**|**sys.database_principals**|  
|**uid**|**syscacheobjects**|**sys.dm_exec_plan_attributes**|  
|**uid**|**sysprocesses**|**sys.dm_exec_requests**|  
  
 ユーザーデータベースで参照されている場合、SQL Server 2000 で非推奨と発表されたシステムテーブル ( **sys.syslanguages** や **syscacheobjects**など) は、 **sys** スキーマのバック互換ビューにバインドされるようになりました。 SQL Server 2000 システムテーブルは複数のバージョンで非推奨とされているため、この変更は互換性に影響する変更とは見なされません。  
  
 例: ユーザーが **sys.syslanguages** という名前のユーザーテーブルをユーザーデータベースに作成した場合、SQL Server 2008 では、そのデータベースのステートメントによって、 `SELECT * from dbo.syslanguages;` ユーザーテーブルから値が返されます。 SQL Server 2012 以降、この方法ではシステムビュー **sys.sysの言語**からデータが返されます。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
