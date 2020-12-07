---
description: sp_xtp_merge_checkpoint_files (Transact-sql)
title: sp_xtp_merge_checkpoint_files (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9bd8cf3735ecc240a0d99929fc0ef1c40d931887
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541058"
---
# <a name="syssp_xtp_merge_checkpoint_files-transact-sql"></a>sp_xtp_merge_checkpoint_files (Transact-sql)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  指定されたトランザクション範囲内のすべてのデータファイルとデルタファイルは、sp_xtp_merge_checkpoint_files によってマージされ**ます。**  
  
 詳細については、「 [メモリ最適化オブジェクトのストレージの作成と管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**注**: このストアドプロシージャは、では非推奨とされ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ます。 これは不要になったため、使用できません [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 。|  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 マージを呼び出す対象のデータベースの名前。 データベースにインメモリ テーブルがない場合、このプロシージャはユーザー エラーを返します。 データベースがオフラインの場合は、エラーが返されます。  
  
 *lower_bound_Tid*  
 Dm_db_xtp_checkpoint_files に示すように、データファイルのトランザクションの (bigint) 下限下限は、マージの開始チェックポイントファイルに対応する[transact-sql&#41;&#40;ます。](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) 無効な transactonId 値に対してエラーが生成されました。  
  
 *upper_bound_Tid*  
 [SQL&#41;&#40;dm_db_xtp_checkpoint_files](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)に示すように、データファイルのトランザクションの (bigint) 上限。 無効な transactonId 値に対してエラーが生成されました。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="cursors-returned"></a>返されるカーソル  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールと db_owner 固定データベース ロールが必要です。  
  
## <a name="remarks"></a>解説  
 有効な範囲内のすべてのデータとデルタ ファイルをマージして、1 つのデータとデルタ ファイルを生成します。 この手順は、マージポリシーには適用されません。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
