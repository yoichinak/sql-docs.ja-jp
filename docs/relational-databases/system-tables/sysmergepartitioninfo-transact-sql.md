---
description: sysmergepartitioninfo (Transact-sql)
title: sysmergepartitioninfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfo_TSQL
- sysmergepartitioninfo
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfo system table
ms.assetid: 7429ad2c-dd33-4f7d-89cc-700e083af518
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2b9505763400dbb6bc0cfd98844ee73740353ca5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540811"
---
# <a name="sysmergepartitioninfo-transact-sql"></a>sysmergepartitioninfo (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  各アーティクルのパーティションに関する情報を提供します。 ローカルデータベースで定義されているマージアーティクルごとに1行のデータを格納します。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**uniqueidentifier**|指定されたアーティクルの一意の識別番号。|  
|**pubid**|**uniqueidentifier**|このパブリケーションの一意な識別番号です。パブリケーションが追加されるときに生成されます。|  
|**partition_view_id**|**int**|このテーブルに関するパーティション ビューの ID です。 ビューには、アーティクル内の各行と、それが属している別のパーティション id とのマッピングが表示されます。|  
|**repl_view_id**|**int**|追加されます。|  
|**partition_deleted_view_rule**|**nvarchar (4000)**|マージ レプリケーション トリガー内で、列の古い値に基づいて削除または更新された各行のパーティション ID を取得するために使用される SQL ステートメントです。|  
|**partition_inserted_view_rule**|**nvarchar (4000)**|マージレプリケーショントリガー内で使用される SQL ステートメントは、新しい列値に基づいて挿入または更新された各のパーティション ID を取得します。|  
|**membership_eval_proc_name**|**sysname**|**MSmerge_contents**内の行の現在のパーティション id を評価するプロシージャの名前。|  
|**column_list**|**nvarchar (4000)**|アーティクルでレプリケートされた列のコンマ区切りの一覧です。|  
|**column_list_blob**|**nvarchar (4000)**|Binary Large Object の列を含む、アーティクル内でレプリケートされた列のコンマ区切りの一覧です。|  
|**expand_proc**|**sysname**|新しく挿入された親行のすべての子行のパーティション Id を再評価するプロシージャの名前。または、パーティションの変更または削除が行われた親行の場合。|  
|**logical_record_parent_nickname**|**int**|論理レコード内の特定のアーティクルの最上位レベルの親のニックネーム。|  
|**logical_record_view**|**int**|それぞれの子の rowguid に対応する、トップレベルにある親アーティクルの rowguid を出力するビューです。|  
|**logical_record_deleted_view_rule**|**nvarchar (4000)**|**Logical_record_view**に似ていますが、update トリガーと delete トリガーの "deleted" テーブルに子行が表示される点が異なります。|  
|**logical_record_level_conflict_detection**|**bit**|競合を、論理レコード レベルと、行または列レベルのどちらで検出するかを示します。<br /><br /> **0** = 行レベルまたは列レベルの競合検出が使用されます。<br /><br /> **1** = 論理レコードの競合検出が使用されます。この場合、パブリッシャーでの行の変更と、サブスクライバーでの同じ論理レコードの変更は競合として処理されます。<br /><br /> この値が **1**の場合は、論理レコードレベルの競合解決だけを使用できます。|  
|**logical_record_level_conflict_resolution**|**bit**|競合を、論理レコード レベルと、行または列レベルのどちらで解決するかを示します。<br /><br /> **0** = 行または列レベルの解決が使用されます。<br /><br /> **1** = 競合が発生した場合、勝者からの論理レコード全体が、損失側の論理レコード全体を上書きします。<br /><br /> 値 **1** は、論理レコードレベルの検出と、行レベルまたは列レベルの検出の両方で使用できます。|  
|**partition_options**|**tinyint**|アーティクル内のデータをパーティション分割する方法を定義します。これにより、すべての行が1つのパーティションまたは1つのサブスクリプションのみに属している場合に、パフォーマンスを最適化できます。 *partition_options* 、次のいずれかの値を指定できます。<br /><br /> **0** = アーティクルのフィルター選択は静的であるか、またはパーティションごとに一意のデータのサブセットを生成しません。つまり "重複する" パーティションです。<br /><br /> **1** = パーティションは重複しており、サブスクライバーで行われた DML の更新では、行が属するパーティションを変更することはできません。<br /><br /> **2** = アーティクルのフィルター選択によって重複しないパーティションが生成されますが、複数のサブスクライバーが同じパーティションを受け取ることができます。<br /><br /> **3** = アーティクルのフィルター選択により、各サブスクリプションで一意な重複しないパーティションが生成されます。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
