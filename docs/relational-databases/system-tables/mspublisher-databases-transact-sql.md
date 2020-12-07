---
description: MSpublisher_databases (Transact-SQL)
title: MSpublisher_databases (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: caba0fa6bf5bee0d00b182a82fc2add0c5061720
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550985"
---
# <a name="mspublisher_databases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSpublisher_databases**テーブルには、ローカルディストリビューターによって処理されるパブリッシャー/パブリッシャーデータベースのペアごとに1行のデータが格納されます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**id**|**int**|行の ID。|  
|**publisher_engine_edition**|**int**|パブリッシャーのエディション [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。次のいずれかになります。<br /><br /> **10** = Personal Edition<br /><br /> **11** = デスクトップエンジン (MSDE)<br /><br /> **20** = 標準<br /><br /> **21** = ワークグループ<br /><br /> **30** = Enterprise (評価版)<br /><br /> **31** = Developer<br /><br /> **40** = Express (express をパブリッシャーにすることはできません。 この値は、完全を期すために用意されています)。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
