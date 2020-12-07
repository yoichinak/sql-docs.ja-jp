---
description: MSreplmonthresholdmetrics (Transact-sql)
title: MSreplmonthresholdmetrics (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 63006d1f481ba512a78ee73208c39206d0d19ff9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89524321"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplmonthresholdmetrics**テーブルは、レプリケーションを監視するために提供されるメトリックを定義します。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|レプリケーションパフォーマンスメトリックを識別します。次のいずれかの値を指定できます。<br /><br /> **1** = 有効期限<br /><br /> **2** = 待機時間<br /><br /> **4** = mergeexpiration 期限<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|レプリケーション パフォーマンス基準の名前。|  
|**warningbitstatus**|**int**|次のいずれかの基準に対応するしきい値違反の警告を示す、ビットごとの識別子です。<br /><br /> **1** = 有効期限-トランザクションパブリケーションへのサブスクリプションが、保有期間の割合として、許容されるしきい値を超える保有期間を超えました。<br /><br /> **2** = 待機時間-トランザクションパブリッシャーからサブスクライバーへのデータのレプリケートにかかった時間が、秒単位のしきい値を超えています。<br /><br /> **4** = mergeexpiration-マージパブリケーションに対するサブスクリプションが、保有期間の割合として許容されるしきい値を超える保有期間を超えました。<br /><br /> **8** = mergefastrunduration-高速ネットワーク接続経由で、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **16** = mergeslowrunduration-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **32** = mergefastrunspeed-高速ネットワーク接続上で、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でのしきい値の比率を維持できませんでした。<br /><br /> **64** = mergeslowrunspeed-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でしきい値を維持できませんでした。|  
|**alertmessageid**|**int**|しきい値の警告が発生した場合に表示されるエラー メッセージの ID。|  
|**description**|**nvarchar (3000)**|レプリケーションパフォーマンス基準の説明|  
|**default_value**|**sql_variant**|レプリケーション パフォーマンス基準の既定値。|  
|**min_value**|**sql_variant**|範囲指定されたレプリケーションパフォーマンスメトリックの最小値。|  
|**max_value**|**sql_variant**|範囲指定されたレプリケーションパフォーマンスメトリックの最大値です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
