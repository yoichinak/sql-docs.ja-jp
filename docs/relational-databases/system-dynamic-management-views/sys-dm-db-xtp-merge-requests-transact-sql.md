---
description: sys.dm_db_xtp_merge_requests (Transact-sql)
title: sys.dm_db_xtp_merge_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 7a7f8f4a38bffb8abc6be1380a2225077130f143
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98099862"
---
# <a name="sysdm_db_xtp_merge_requests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-sql)

[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

データベースのマージ要求を追跡します。 Merge 要求が SQL Server によって生成されたか、 [sys.sp_xtp_merge_checkpoint_files (transact-sql)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)を使用しているユーザーが要求を作成した可能性があります。

> [!NOTE]
> この動的管理ビュー (DMV) sys.dm_db_xtp_merge_requests は、Microsoft SQL Server 2014 まで存在します。
> ただし、SQL Server 2016 以降では、この DMV は適用されなくなりました。

## <a name="columns-in-the-report"></a>レポート内の列

| 列名 | データ型 | 説明 |
| :-- | :-- | :-- |
| request_state | tinyint | マージ要求の状態。<br/>0 = 要求<br/>1 = 保留中<br/>2 = インストール済み<br/>3 = 破棄済み |
| request_state_desc | nvarchar(60) | 要求の現在の状態の意味:<br/><br/>要求-マージ要求が存在します。<br/>保留中-マージを処理しています。<br/>Installed-マージが完了しました。<br/>破棄-ストレージが不足しているため、マージを完了できませんでした。 |
| destination_file_id | GUID | マージ元ファイルのマージ先ファイルの一意識別子。 |
| lower_bound_tsn | bigint | マージ先ファイルの最小のタイムスタンプ。 マージするすべてのソースファイルの最小トランザクションタイムスタンプ。 |
| upper_bound_tsn | bigint | マージ先ファイルの最大のタイムスタンプ。 マージするすべてのソースファイルの最大トランザクションタイムスタンプ。 |
| collection_tsn | bigint | 現在の行を収集できるタイムスタンプ。<br/><br/>Checkpoint_tsn が collection_tsn を超えると、インストールされている状態の行が削除されます。<br/><br/>Abandoned 状態の行は、checkpoint_tsn が collection_tsn より小さいと削除されます。 |
| checkpoint_tsn | bigint | チェックポイントが開始された時刻。<br/><br/>この値より低いタイムスタンプを持つトランザクションによって実行されるすべての削除は、新しいデータファイルに含まれます。 残りの削除は、ターゲットデルタファイルに移動されます。 |
| sourcenumber_file_id | GUID | マージ内のソースファイルを一意に識別する、最大16の内部ファイル Id。 |

## <a name="permissions"></a>アクセス許可

現在のデータベースに対する VIEW DATABASE STATE 権限が必要です。

## <a name="see-also"></a>関連項目

[メモリ最適化テーブルの動的管理ビュー (Transact-sql)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
