---
description: IHarticles (Transact-sql)
title: IHarticles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fc67de5d66f897ccc54a1cc06cf88aac35e572b5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540971"
---
# <a name="iharticles-transact-sql"></a>IHarticles (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHarticles**システムテーブルには、現在のディストリビューターを使用して SQL Server 以外のパブリッシャーからレプリケートされているアーティクルごとに1行の値が格納されます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|アーティクルの一意な ID 番号を示す ID 列です。|  
|**name**|**sysname**|アーティクルに関連付けられた名前です。パブリケーション内で一意です。|  
|**publication_id**|**smallint**|アーティクルが属しているパブリケーションの ID。|  
|**table_id**|**int**|[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)からパブリッシュされるテーブルの ID。|  
|**publisher_id**|**smallint**|SQL&#xA0;Server 以外のパブリッシャーの ID です。|  
|**creation_script**|**nvarchar (255)**|アーティクルのスキーマスクリプトです。|  
|**del_cmd**|**nvarchar (255)**|テーブル アーティクルの削除をレプリケートするときに使用されるレプリケーション コマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**filter**|**int**|この列は使用されず、SQL Server アーティクル ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)) に使用される[Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) view と**IHarticles**テーブルの[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)ビューとの互換性を確保するためだけに含まれています。|  
|**filter_clause**|**ntext**|アーティクルの WHERE 句は、行方向のフィルター選択に使用され、SQL 以外のパブリッシャーによって解釈できる標準の Transact-sql で記述されます。|  
|**ins_cmd**|**nvarchar (255)**|Insert をテーブルアーティクルと共にレプリケートするときに使用されるレプリケーションコマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**pre_creation_cmd**|**tinyint**|同じ名前のオブジェクトがサブスクライバーに既に存在する場合に、初期スナップショットが適用される前に実行するコマンドです。<br /><br /> **0** = なし-コマンドは実行されません。<br /><br /> **1** = ドロップダウンテーブルを削除します。<br /><br /> **2** = 削除-変換先テーブルからデータを削除します。<br /><br /> **3** = 切り捨て-変換先テーブルを切り捨てます。|  
|**status**|**tinyint**|アーティクルのオプションと状態のビットマスク。これらの値の1つ以上のビットごとの論理和演算を実行できます。<br /><br /> **0** = 追加のプロパティはありません。<br /><br /> **1** = アクティブ。<br /><br /> **8** = INSERT ステートメントに列名を含めます。<br /><br /> **16** = パラメーター化されたステートメントを使用します。<br /><br /> たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの場合、この列の値は17になります。 値0は、アーティクルが非アクティブであり、追加のプロパティが定義されていないことを示します。|  
|**type**|**tinyint**|アーティクルのタイプです。<br /><br /> **1** = ログベースのアーティクル。|  
|**upd_cmd**|**nvarchar (255)**|テーブルアーティクルで更新をレプリケートするときに使用されるレプリケーションコマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**schema_option**|**binary (8)**|指定されたアーティクルに対するスキーマ生成オプションのビットマップです。次に示す 1 つ以上の値のビットごとの論理和演算をとります。<br /><br /> **0x00** = スナップショットエージェントによるスクリプト作成を無効にし、提供されたスクリプトを使用します。<br /><br /> **0x01** = オブジェクトの作成 (CREATE TABLE、CREATE PROCEDURE など) を生成します。<br /><br /> **0x10** = 対応するクラスター化インデックスを生成します。<br /><br /> **0x40** = 対応する非クラスター化インデックスを生成します。<br /><br /> **0x80** = 宣言された参照整合性を主キーに含めます。<br /><br /> **0x1000** = 列レベルの照合順序をレプリケートします。 注: このオプションは、大文字と小文字を区別する比較を有効にするために、Oracle パブリッシャーに対して既定で設定されます。<br /><br /> **0x4000** = テーブルアーティクルで定義されている場合は、一意キーをレプリケートします。<br /><br /> **0x8000** = ALTER table ステートメントを使用して、テーブルアーティクル上の主キーと一意キーを制約としてレプリケートします。|  
|**dest_owner**|**sysname**|転送先データベースのテーブルの所有者を指定します。|  
|**dest_table**|**sysname**|対象テーブルの名前です。|  
|**tablespace_name**|**nvarchar (255)**|アーティクルのログ テーブルによって使用されるテーブルスペースを識別します。|  
|**objid**|**int**|この列は使用されず、SQL Server アーティクル ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)) に使用される[Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) view と**IHarticles**テーブルの[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)ビューとの互換性を確保するためだけに含まれています。|  
|**sync_objid**|**int**|この列は使用されず、SQL Server アーティクル ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)) に使用される[Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) view と**IHarticles**テーブルの[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)ビューとの互換性を確保するためだけに含まれています。|  
|**description**|**nvarchar (255)**|アーティクルの説明エントリです。|  
|**publisher_status**|**int**|パブリッシュされたアーティクルを定義するビューが [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)を呼び出すことによって定義されているかどうかを示すために使用します。<br /><br /> **0**  = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)が呼び出されました。<br /><br /> **1**  = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)が呼び出されていません。|  
|**article_view_owner**|**nvarchar (255)**|ログ リーダー エージェントによって使用されるパブリッシャー上の同期オブジェクトの所有者です。|  
|**article_view**|**nvarchar (255)**|ログ リーダー エージェントによって使用されるパブリッシャー上の同期オブジェクトです。|  
|**ins_scripting_proc**|**int**|この列は使用されず、SQL Server アーティクル ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)) に使用される[Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) view と**IHarticles**テーブルの[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)ビューとの互換性を確保するためだけに含まれています。|  
|**del_scripting_proc**|**int**|この列は使用されず、SQL Server アーティクル ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)) に使用される[Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) view と**IHarticles**テーブルの[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)ビューとの互換性を確保するためだけに含まれています。|  
|**upd_scripting_proc**|**int**|この列は使用されず、SQL Server アーティクル ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)) に使用される[Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) view と**IHarticles**テーブルの[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)ビューとの互換性を確保するためだけに含まれています。|  
|**custom_script**|**int**|この列は使用されず、SQL Server アーティクル ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)) に使用される[Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) view と**IHarticles**テーブルの[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)ビューとの互換性を確保するためだけに含まれています。|  
|**fire_triggers_on_snapshot**|**bit**|この列は使用されず、SQL Server アーティクル ([sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)) に使用される[Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) view と**IHarticles**テーブルの[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)ビューとの互換性を確保するためだけに含まれています。|  
|**instance_id**|**int**|パブリッシュされたテーブルのアーティクルログの現在のインスタンスを識別します。|  
|**use_default_datatypes**|**bit**|アーティクルが既定のデータ型マッピングを使用するかどうかを示します。値 **1** は、既定のデータ型マッピングが使用されることを示します。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
