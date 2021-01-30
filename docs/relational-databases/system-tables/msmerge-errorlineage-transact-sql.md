---
description: MSmerge_errorlineage (Transact-sql)
title: MSmerge_errorlineage (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSmerge_errorlineage_TSQL
- MSmerge_errorlineage
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_errorlineage system table
ms.assetid: 3bcbd328-c958-4cd4-a573-3c35539fa919
author: cawrites
ms.author: chadam
ms.openlocfilehash: 9dcf7f8db0a5d02a64657e00046667b07d1e29e3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99171679"
---
# <a name="msmerge_errorlineage-transact-sql"></a>MSmerge_errorlineage (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_errorlineage** テーブルには、サブスクライバーで削除された行が含まれていますが、その削除はパブリッシャーに反映されていません。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|マージレプリケーション用にパブリッシュされたテーブルに割り当てられた整数値。 **Sysmergearticles** テーブルの [ニックネーム] フィールドに対応します。|  
|**rowguid**|**uniqueidentifier**|行識別子。|  
|**継承**|**varbinary (501)**|行の更新を行ったサブスクライバーとパブリッシャーの履歴リストを格納します。 競合の状況を検出して解決するために使用されます。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
