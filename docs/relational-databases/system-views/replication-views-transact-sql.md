---
title: レプリケーションビュー (Transact-sql) |Microsoft Docs
description: レプリケーションビューには SQL Server のレプリケーションで使用される情報が含まれます。 これらのビューでは、レプリケーション システム テーブルのデータに、容易にアクセスできます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- distribution databases [SQL Server replication], system views
- metadata [SQL Server], views
- views [SQL Server], replication
- replication views [SQL Server]
- publications [SQL Server replication], system views
- articles [SQL Server replication], system views
- replication metadata [SQL Server]
- subscriptions [SQL Server replication], system views
- system views [SQL Server], replication
ms.assetid: 93e5056d-0d93-4a48-ba33-72762eb995d8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 64fcd7c57c57dec9978695b52db1af2cc2c8ebba
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160360"
---
# <a name="replication-views-transact-sql"></a>レプリケーションビュー (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  これらのビューには、のレプリケーションで使用される情報が含まれて [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] います。 ビューを使用すると、 [レプリケーションシステムテーブル](../../relational-databases/system-tables/replication-tables-transact-sql.md)のデータに簡単にアクセスできます。 ビューは、データベースがパブリケーションまたはサブスクリプションデータベースとして有効になっている場合に、ユーザーデータベースに作成されます。 データベースがレプリケーショントポロジから削除されると、すべてのレプリケーションオブジェクトがユーザーデータベースから削除されます。 レプリケーションメタデータにアクセスするには、 [レプリケーションストアドプロシージャ](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)を使用することをお勧めします。  
  
> [!IMPORTANT]  
>  システムビューは、ユーザーが直接変更することはできません。  
  
## <a name="replication-views"></a>レプリケーション ビュー  
 次に示すのは、レプリケーションで使用されるシステムビューの一覧で、データベースごとにグループ化されています。  
  
### <a name="replication-views-in-the-msdb-database"></a>msdb データベースのレプリケーション ビュー  

:::row:::
    :::column:::
        [MSdatatype_mappings &#40;Transact-sql&#41;](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)
    :::column-end:::
    :::column:::
        [msdb.dbo.sysdatatypemappings &#40;Transact-sql&#41;](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="replication-views-in-the-distribution-database"></a>ディストリビューション データベースのレプリケーション ビュー  

:::row:::
    :::column:::
        [IHextendedArticleView &#40;Transact-sql&#41;](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)

        [IHextendedSubscriptionView &#40;Transact-sql&#41;](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)

        [IHsyscolumns &#40;Transact-sql&#41;](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)

        [MSdistribution_status &#40;Transact-sql&#41;](../../relational-databases/system-views/msdistribution-status-transact-sql.md)

        [sysarticlecolumns &#40;システムビュー&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)
    :::column-end:::
    :::column:::
        [sysarticles &#40;システムビュー&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)

        [sysextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)

        [syspublications &#40;システム ビュー&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)

        [syssubscriptions &#40;システム ビュー&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="replication-views-in-the-publication-database"></a>パブリケーションデータベースのレプリケーションビュー  

:::row:::
    :::column:::
        [sysmergeextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)

        [systranschemas &#40;Transact-sql&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)
    :::column-end:::
    :::column:::
        [sysmergepartitioninfoview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="replication-views-in-the-subscription-database"></a>サブスクリプション データベースのレプリケーション ビュー  

:::row:::
    :::column:::
        [sysmergeextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)

        [sysmergepartitioninfoview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)
    :::column-end:::
    :::column:::
        [systranschemas &#40;Transact-sql&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
