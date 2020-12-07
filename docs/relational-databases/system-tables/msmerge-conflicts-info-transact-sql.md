---
description: MSmerge_conflicts_info (Transact-SQL)
title: MSmerge_conflicts_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflicts_info_TSQL
- MSmerge_conflicts_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflicts_info system table
ms.assetid: 6b76ae96-737a-4000-a6b6-fcc8772c2af4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5983e002f21a5c30c34dc791ab13e4784fd96c99
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545697"
---
# <a name="msmerge_conflicts_info-transact-sql"></a>MSmerge_conflicts_info (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_conflicts_info**テーブルは、サブスクリプションをマージパブリケーションと同期するときに発生する競合を追跡します。 競合している行データの損失は、競合が発生したアーティクルの [MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md) テーブルに格納されます。 このテーブルは、パブリッシャー側のパブリケーションデータベースに格納され、サブスクライバー側のサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|パブリッシュされたテーブルのニックネーム。|  
|**rowguid**|**uniqueidentifier**|競合している行の識別子です。|  
|**origin_datasource**|**nvarchar (255)**|競合している変更が発生したデータベースの名前です。|  
|**conflict_type**|**int**|発生した競合の種類。次のいずれかを指定できます。<br /><br /> **1** = 更新の競合: 行レベルで競合が検出されます。<br /><br /> **2** = 列更新の競合: 列レベルで競合が検出されました。<br /><br /> **3** = 更新の削除 Wins の競合: 削除によって競合が優先されます。<br /><br /> **4** = 更新 Wins 削除の競合: 競合が失われた削除済みの rowguid がこのテーブルに記録されます。<br /><br /> **5** = 挿入のアップロードに失敗しました: サブスクライバーからの挿入をパブリッシャーで適用できませんでした。<br /><br /> **6** = ダウンロードの挿入に失敗しました: パブリッシャーからの挿入をサブスクライバーで適用できませんでした。<br /><br /> **7** = 削除のアップロードに失敗しました: サブスクライバーでの削除をパブリッシャーにアップロードできませんでした。<br /><br /> **8** = 削除のダウンロードに失敗: パブリッシャーでの削除をサブスクライバーにダウンロードできませんでした。<br /><br /> **9** = 更新のアップロードに失敗しました: サブスクライバーでの更新をパブリッシャーで適用できませんでした。<br /><br /> **10** = 更新のダウンロードに失敗しました: パブリッシャーでの更新をサブスクライバーに適用できませんでした。<br /><br /> **11** = 解決策<br /><br /> **12** = 論理レコードの更新による Wins の削除: 競合が失われた削除された論理レコードがこのテーブルに記録されます。<br /><br /> **13** = 論理レコードの競合の挿入更新: 論理レコードへの挿入が更新と競合しています。<br /><br /> **14** = 論理レコードの削除 Wins 更新の競合: 競合が失われる更新された論理レコードがこのテーブルに記録されます。|  
|**reason_code**|**int**|状況に依存する可能性があるエラーコード。 更新-更新および更新-削除の競合の場合、この列に使用される値は **conflict_type**と同じになります。 ただし、失敗した変更の競合については、理由コードは、マージエージェントが変更を適用できない原因となったエラーです。 たとえば、主キー違反のためにマージエージェントがサブスクライバーで挿入を適用できない場合、6の **conflict_type** ("download insert failed") と2627の **reason_code** がログに記録されます。これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主キー違反の内部エラーメッセージです。 "% ls 制約 '%. * ls ' の違反です。 オブジェクト '% には重複するキーを挿入できません。 \*ls '. "|  
|**reason_text**|**nvarchar (720)**|状況に依存する可能性があるエラーの説明。|  
|**pubid**|**uniqueidentifier**|パブリケーションの識別子。|  
|**MSrepl_create_time**|**datetime**|競合が発生した時刻。|  
|**origin_datasource_id**|**uniqueidentifier**|競合する変更が発生したデータベースの識別子。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
