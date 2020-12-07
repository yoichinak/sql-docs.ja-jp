---
description: MSmerge_settingshistory (Transact-sql)
title: MSmerge_settingshistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 841f2986d09bd048f857e45a8bde3c5db6d0fc70
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545605"
---
# <a name="msmerge_settingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_settingshistory**テーブルは、マージレプリケーションのアーティクルおよびパブリケーションのプロパティに加えられた変更の履歴を保持するために使用され、マージレプリケーショントポロジに対して行われた変更ごとに1行のデータを保持します。 このテーブルには、プロパティの初期設定が行われたタイミングに関する情報も格納されます。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**eventtime**|**datetime**|イベントが発生した日時。|  
|**pubid**|**uniqueidentifier**|指定されたパブリケーションの一意の id 番号です。|  
|**artid**|**uniqueidentifier**|指定されたアーティクルの一意の識別番号。|  
|**eventtype**|**tinyint**|記録されるイベントの種類を指定します。次のいずれかを指定できます。<br /><br /> **1** -パブリケーションレベルのプロパティの初期設定。<br /><br /> **2** -パブリケーションのプロパティを変更します。<br /><br /> **101** -最初のアーティクルプロパティの設定。<br /><br /> **102** -アーティクルのプロパティを変更します。|  
|**propertyname**|**sysname**|設定または変更されたプロパティの名前|  
|**previousvalue**|**sysname**|プロパティが変更された場合は、前のプロパティ値。|  
|**newvalue**|**sysname**|変更後または作成時のプロパティの値。|  
|**eventtext**|**nvarchar (2000)**|イベントを説明する文字列。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
