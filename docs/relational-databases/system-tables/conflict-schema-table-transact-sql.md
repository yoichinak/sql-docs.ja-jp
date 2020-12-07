---
description: conflict_ &lt; schema &gt; _ &lt; table &gt; (transact-sql)
title: conflict_ &lt; schema &gt; _ &lt; table &gt; (transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/15/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- conflict_
- conflict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conflict_<schema>_<table>
ms.assetid: 15ddd536-db03-454e-b9b5-36efe1f756d7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 126474b4efe2eafb5c235d1ba4a31e433d71500c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544668"
---
# <a name="conflict_ltschemagt_lttablegt-transact-sql"></a>conflict_ &lt; schema &gt; _ &lt; table &gt; (transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Conflict_ _ テーブルには、 \<schema> \<table> ピアツーピアレプリケーションの競合する行に関する情報が含まれています。 競合テーブルはパブリケーション内のレプリケートされたテーブルごとに存在し、競合テーブルの名前にはスキーマとアーティクルの名前が付加されます。 このアーティクル固有の競合テーブルは、各パブリケーション データベースに保存されます。  
  
 ピア ツー ピア レプリケーションの場合、ディストリビューション エージェントは、競合を検出すると既定で停止します。 競合エラーはエラー ログに記録されますが、競合データは競合テーブルに記録されないため、競合データを表示できません。 ディストリビューション エージェントが実行の継続を許可されている場合は、競合が検出された各ノードで、競合がローカルでログに記録されます。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」の「競合の処理」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|__$originator_id|**int**|競合する変更が発生したノードの ID。 Id の一覧を表示するには、 [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md)を実行します。|  
|__$origin_datasource|**int**|競合する変更が発生したノード。|  
|__$tranid|**nvarchar (40)**|__$origin_datasource で適用されたときの競合する変更のログ シーケンス番号 (LSN) です。|  
|__$conflict_type|**int**|競合の種類。次のいずれかの値を指定できます。<br /><br /> 1: ローカル行が別の更新によって変更されたか、削除されてから再挿入されたため、更新に失敗しました。<br /><br /> 2: ローカル行が既に削除されていたため、更新に失敗しました。<br /><br /> 3: ローカル行が別の更新によって変更されたか、削除された後に再挿入されたため、削除できませんでした。<br /><br /> 4: ローカル行が既に削除されていたため、削除に失敗しました。<br /><br /> 5: ローカル行が既に挿入されているか、挿入されてから更新されたため、挿入に失敗しました。|  
|__$is_winner|**bit**|このテーブルの行が競合の優先であるかどうかを示します。これは、ローカルノードに適用されたことを意味します。|  
|__$pre_version|**varbinary (32)**|競合する変更が発生したデータベースのバージョン。|  
|__$reason_code|**int**|競合の解決コード。 次の値のいずれかです。<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> <br /><br /> 詳細については、「 **__ $ reason_text**」を参照してください。|  
|__$reason_text|**nvarchar (720)**|競合の解決策。 次の値のいずれかです。<br /><br /> 解決 (1)<br /><br /> 未解決 (2)<br /><br /> 不明 (0)|  
|__$update_bitmap|**varbinary (** *n* **)**。 サイズはコンテンツによって異なります。|更新 - 更新の競合が発生した場合にどの列が更新されたかを示すビットマップです。|  
|__$inserted_date|**datetime**|競合している行がこのテーブルに挿入された日付と時刻。|  
|__$row_id|**timestamp**|競合の原因となった行に関連付けられている行バージョン。|  
|__$change_id|**binary (8)**|ローカル行の場合、この値はローカル行と競合している挿入行の __$row_id に等しくなります。 この値は、受信行の場合は NULL です。|  
|\<base table column names>|\<base table column types>|競合テーブルには、ベーステーブルの列ごとに1つの列が含まれています。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
