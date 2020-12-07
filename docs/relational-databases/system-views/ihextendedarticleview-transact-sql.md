---
description: IHextendedArticleView (Transact-SQL)
title: IHextendedArticleView (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a56d2e7b96464866f0216e1f93ef6eb3d1066df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463874"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHextendedArticleView**ビューでは、SQL Server 以外のパブリケーションのアーティクルに関する情報が公開されます。 このビューは、 **ディストリビューション** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|パブリッシャーの一意の識別子。|  
|**publication_id**|**int**|パブリケーションの一意識別子です。|  
|**記事**|**sysname**|アーティクルの名前|  
|**destination_object**|**sysname**|サブスクライバー側でパブリッシュされたオブジェクトの名前。|  
|**source_owner**|**sysname**|パブリッシャー側でパブリッシュされたオブジェクトの所有者です。|  
|**source_object**|**sysname**|パブリッシャーでパブリッシュされたオブジェクトの名前。|  
|**description**|**nvarchar (255)**|アーティクルの説明です。|  
|**creation_script**|**nvarchar (255)**|アーティクルのスキーマ作成スクリプトです。|  
|**del_cmd**|**nvarchar (255)**|削除のために実行されるコマンドです。|  
|**filter**|**int**|行方向のパーティション分割を定義するために使用するストアド プロシージャの識別子です。|  
|**filter_clause**|**ntext**|アーティクルを行方向にフィルター選択するために使用する WHERE 句です。|  
|**ins_cmd**|**nvarchar (255)**|挿入のために実行されるコマンドです。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE、または TRUNCATE の事前作成コマンド。<br /><br /> **0** = なし。<br /><br /> **1** = DROP。<br /><br /> **2** = 削除します。<br /><br /> **3** = 切り捨て。|  
|**status**|**tinyint**|アーティクルのオプションと状態のビットマスク。これらの値の1つ以上のビットごとの論理和演算を実行できます。<br /><br /> **1** = アーティクルはアクティブです。<br /><br /> **8** = INSERT ステートメントに列名を含めます。<br /><br /> **16** = パラメーター化されたステートメントを使用します。<br /><br /> **24** = INSERT ステートメントに列名を含め、パラメーター化されたステートメントを使用します。<br /><br /> たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの場合、この列の値は **17** になります。 値 **0** は、アーティクルが非アクティブであり、追加のプロパティが定義されていないことを示します。|  
|**type**|**tinyint**|アーティクルの種類:<br /><br /> **1** = ログベースのアーティクル。<br /><br /> **3** = 手動フィルターを使用したログベースのアーティクル。<br /><br /> **5** = 手動ビューを使用したログベースのアーティクル。<br /><br /> **7** = 手動フィルターと手動ビューを使用するログベースのアーティクル。|  
|**upd_cmd**|**nvarchar (255)**|更新プログラムに対して実行されるコマンドです。|  
|**schema_option**|**[バイナリ]**|スクリプト化の対象を示します。サポートされているスキーマオプションの一覧については、「 [sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 」を参照してください。|  
|**dest_owner**|**sysname**|転送先データベースのパブリッシュされたオブジェクトの所有者です。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
