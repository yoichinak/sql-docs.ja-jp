---
description: sysmergeschemaarticles (Transact-SQL)
title: sysmergeschemaarticles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 690ffd7f583c008ff68138211f3181b607a1687b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547065"
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージレプリケーションのスキーマのみのアーティクルを追跡します。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|マージパブリケーション内のスキーマのみのアーティクルの名前です。|  
|**type**|**tinyint**|スキーマのみのアーティクルの種類を示します。次のいずれかを指定できます。<br /><br /> **0x20** = ストアドプロシージャのスキーマのみのアーティクル。<br /><br /> **0x40** = ビュースキーマのみのアーティクルまたはインデックス付きビューのスキーマのみのアーティクル。|  
|**objid**|**int**|アーティクルベースオブジェクトのオブジェクト識別子。 には、プロシージャ、ビュー、インデックス付き、ビュー、またはユーザー定義関数のオブジェクト識別子を指定できます。|  
|**artid**|**uniqueidentifier**|アーティクル ID です。|  
|**description**|**nvarchar (255)**|アーティクルの説明です。|  
|**pre_creation_command**|**tinyint**|サブスクリプション データベースの中でアーティクルが作成されるときに実行される既定の操作。<br /><br /> **0 =** なし-サブスクライバーにテーブルが既に存在する場合、アクションは実行されません。<br /><br /> **1** = Drop-テーブルを再作成する前に削除します。<br /><br /> **2** = 削除-サブセットフィルターの WHERE 句に基づいて削除を発行します。<br /><br /> **3** = 切り捨て- **2**と同じですが、行ではなくページを削除します。 ただし、は WHERE 句を受け取りません。|  
|**pubid**|**uniqueidentifier**|パブリケーションの一意識別子です。|  
|**status**|**tinyint**|スキーマだけのアーティクルの状態。次のいずれかになります。<br /><br /> **1** = 同期されていない-テーブルをパブリッシュする初期処理スクリプトは、次回スナップショットエージェントが実行されるときに実行されます。<br /><br /> **2** = アクティブ-テーブルをパブリッシュする初期処理スクリプトが実行されました。<br /><br /> **5** = New_inactive 追加されます。<br /><br /> **6** = New_active 追加されます。|  
|**creation_script**|**nvarchar (255)**|ターゲット テーブルの作成に使用されるアーティクル スキーマの事前作成スクリプトのパスと名前 (省略可能)。|  
|**schema_option**|**binary (8)**|スキーマだけのアーティクルに関連するスキーマ生成オプションのビットマップ。次の値のうち 1 つ以上の結果を、ビットごとに論理和演算したものになります。<br /><br /> **0x00** = スナップショットエージェントによるスクリプト作成を無効にし、提供されたスクリプトを使用します。<br /><br /> **0x01** = オブジェクトの作成 (CREATE TABLE、CREATE PROCEDURE など) を生成します。<br /><br /> **0x10** = 対応するクラスター化インデックスを生成します。<br /><br /> **0x20** = ユーザー定義データ型を基本データ型に変換します。<br /><br /> **0x40** = 対応する非クラスター化インデックスを生成します。<br /><br /> **0x80** = 宣言された参照整合性を主キーに含めます。<br /><br /> **0x100** = 定義されている場合は、テーブルアーティクルのユーザートリガーをレプリケートします。<br /><br /> **0x200** = 外部キー制約をレプリケートします。 参照先のテーブルがパブリケーションの一部でない場合、パブリッシュされたテーブルのすべての foreign key 制約はレプリケートされません。<br /><br /> **0x400** = check 制約をレプリケートします。<br /><br /> **0x800** = 既定値をレプリケートします。<br /><br /> **0x1000** = 列レベルの照合順序をレプリケートします。<br /><br /> **0x2000** = パブリッシュされたアーティクルのソースオブジェクトに関連付けられた拡張プロパティをレプリケートします。<br /><br /> **0x4000** = テーブルアーティクルで定義されている場合は、一意キーをレプリケートします。<br /><br /> **0x8000** = ALTER table ステートメントを使用して、テーブルアーティクル上の主キーと一意キーを制約としてレプリケートします。<br /><br /> **Schema_option**に使用できる値の詳細については、「 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」を参照してください。|  
|**destination_object**|**sysname**|サブスクリプションデータベース内の対象オブジェクトの名前。 この値は、ストアドプロシージャ、ビュー、Udf など、スキーマのみのアーティクルに適用されます。|  
|**destination_owner**|**sysname**|サブスクリプションデータベース内のオブジェクトの所有者 ( **dbo**ではない場合)。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
