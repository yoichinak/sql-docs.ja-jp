---
description: sysarticles (Transact-sql)
title: sysarticles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticles system table
ms.assetid: 9d9d5d51-6d8f-4e42-84a9-82e58eb0301e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 26666dab768a1d029231e81936e7b581a918836d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89517882"
---
# <a name="sysarticles-transact-sql"></a>sysarticles (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ローカルデータベースで定義されているアーティクルごとに1行のデータを格納します。 このテーブルは、パブリッシュされたデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|アーティクルの一意な ID 番号を示す ID 列です。|  
|**creation_script**|**nvarchar (255)**|アーティクルのスキーマスクリプトです。|  
|**del_cmd**|**nvarchar (255)**|テーブル アーティクルの削除をレプリケートするときに使用されるレプリケーション コマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**description**|**nvarchar (255)**|アーティクルの説明エントリです。|  
|**dest_table**|**sysname**|対象テーブルの名前です。|  
|**filter**|**int**|行方向のパーティション分割に使用されるストアドプロシージャの ID です。|  
|**filter_clause**|**ntext**|行方向のフィルター選択に使用される、アーティクルの WHERE 句。|  
|**ins_cmd**|**nvarchar (255)**|Insert をテーブルアーティクルと共にレプリケートするときに使用されるレプリケーションコマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**name**|**sysname**|アーティクルに関連付けられた名前です。パブリケーション内で一意です。|  
|**objid**|**int**|パブリッシュされたテーブルオブジェクト ID です。|  
|**pubid**|**int**|アーティクルが属しているパブリケーションの ID。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE、または TRUNCATE の事前作成コマンド。<br /><br /> **0** = なし。<br /><br /> **1** = DROP。<br /><br /> **2** = 削除します。<br /><br /> **3** = 切り捨て。|  
|**status**|**tinyint**|アーティクルのオプションと状態のビットマスク。これらの値の1つ以上のビットごとの論理和演算を実行できます。<br /><br /> **1** = アーティクルはアクティブです。<br /><br /> **8** = INSERT ステートメントに列名を含めます。<br /><br /> **16** = パラメーター化されたステートメントを使用します。<br /><br /> **24** = INSERT ステートメントに列名を含め、パラメーター化されたステートメントを使用します。<br /><br /> **64** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの場合、この列の値は **17** になります。 値 **0** は、アーティクルが非アクティブであり、追加のプロパティが定義されていないことを示します。|  
|**sync_objid**|**int**|アーティクルの定義を表すテーブルまたはビューの ID です。|  
|**type**|**tinyint**|アーティクルのタイプです。<br /><br /> **1** = ログベースのアーティクル。<br /><br /> **3** = 手動フィルターを使用したログベースのアーティクル。<br /><br /> **5** = 手動ビューを使用したログベースのアーティクル。<br /><br /> **7** = 手動フィルターと手動ビューを使用するログベースのアーティクル。<br /><br /> **8** = ストアドプロシージャの実行。<br /><br /> **24** = シリアル化可能なストアドプロシージャの実行。<br /><br /> **32** = ストアドプロシージャ (スキーマのみ)。<br /><br /> **64** = ビュー (スキーマのみ)。<br /><br /> **128** = 関数 (スキーマのみ)。|  
|**upd_cmd**|**nvarchar (255)**|テーブルアーティクルで更新をレプリケートするときに使用されるレプリケーションコマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**schema_option**|**binary (8)**|アーティクルのスキーマ生成オプションのビットマスク。サブスクライバーに配信するためにスクリプト化されるアーティクルスキーマの部分を制御します。 スキーマ オプションの詳細については、「[sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)」を参照してください。|  
|**dest_owner**|**sysname**|転送先データベースのテーブルの所有者を指定します。|  
|**ins_scripting_proc**|**int**|INSERT ステートメントがレプリケートされるときに実行される登録済みのカスタムストアドプロシージャまたはスクリプト。|  
|**del_scripting_proc**|**int**|DELETE ステートメントがレプリケートされるときに実行される登録済みのカスタムストアドプロシージャまたはスクリプト。|  
|**upd_scripting_proc**|**int**|UPDATE ステートメントがレプリケートされるときに実行される登録済みのカスタム ストアド プロシージャまたはスクリプトです。|  
|**custom_script**|**nvarchar(2048)**|DDL トリガーの最後に実行される登録済みのカスタム ストアド プロシージャまたはスクリプトです。|  
|**fire_triggers_on_snapshot**|**bit**|スナップショットが適用されるときに、レプリケートされたトリガーが実行されるかどうかを示します。次のいずれかの値を指定できます。<br /><br /> **0** = トリガーは実行されません。<br /><br /> **1** = トリガーが実行されます。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)  
  
  
