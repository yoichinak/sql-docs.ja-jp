---
description: MSmerge_tombstone (Transact-SQL)
title: MSmerge_tombstone (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dc137583386c4b098960d762484ef526f2f95f14
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545563"
---
# <a name="msmerge_tombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_tombstone**テーブルには、削除された行に関する情報が含まれており、削除を他のサブスクライバーに反映させることができます。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|行識別子。|  
|**tablenick**|**int**|テーブルのニックネームです。|  
|**type**|**tinyint**|削除の種類。<br /><br /> 1 = ユーザー削除です。<br /><br /> 5 = フィルター選択されたパーティションに既に行が属していません。<br /><br /> 6 = システム削除です。|  
|**継承**|**varbinary (249)**|削除されたレコードのバージョンと、削除されたときに認識された更新を示します。 これによって、あるサブスクライバーによって行が削除されているときに、別のサブスクライバーがこれを更新するという競合を、一貫して回避するための規則が定められます。|  
|**generation**|**int**|は、行が削除されるときに割り当てられます。 サブスクライバーが generation N を要求した場合、generation >= N の廃棄標識だけが送信されます。|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|削除された行が属する論理レコードを識別します。|  
|**logical_record_lineage**|**Varbinary (501)**|この行が属する論理レコードの削除履歴を保持するために使用されるサブスクライバーのニックネームとバージョン番号のペアです。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
