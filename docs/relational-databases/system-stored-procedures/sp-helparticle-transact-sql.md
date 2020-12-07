---
description: sp_helparticle (Transact-sql)
title: sp_helparticle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticle_TSQL
- sp_helparticle
helpviewer_keywords:
- sp_helparticle
ms.assetid: 9c4a1a88-56f1-45a0-890c-941b8e0f0799
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7bc639fef551b78dd73da39cd404999e39219b2d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538796"
---
# <a name="sp_helparticle-transact-sql"></a>sp_helparticle (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  アーティクルに関する情報を表示します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。 Oracle パブリッシャーの場合、このストアドプロシージャは、ディストリビューター側の任意のデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` パブリケーション内のアーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値は **%** です。 *Article*が指定されていない場合は、指定されたパブリケーションのすべてのアーティクルに関する情報が返されます。  
  
`[ @returnfilter = ] returnfilter` フィルター句を返すかどうかを指定します。 *、レプリケーション* は **ビット**,、既定値は **1**,、フィルター句を返します。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーによってパブリッシュされたアーティクルに関する情報を要求するときに、*パブリッシャー*を指定することはできません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @found = ] found OUTPUT` 内部でのみ使用します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**アーティクル id**|**int**|アーティクルの ID。|  
|**アーティクル名**|**sysname**|アーティクルの名前。|  
|**ベース オブジェクト (base object)**|**nvarchar (257)**|アーティクルまたはストアドプロシージャによって表される、基になるテーブルの名前。|  
|**対象オブジェクト**|**sysname**|宛先 (サブスクリプション) テーブルの名前。|  
|**synchronization object**|**nvarchar (257)**|パブリッシュされたアーティクルを定義するビューの名前。|  
|**type**|**smallint**|アーティクルのタイプです。<br /><br /> **1** = ログベース。<br /><br /> **3** = 手動フィルターを使用したログベース。<br /><br /> **5** = ログベースの手動ビュー。<br /><br /> **7** = 手動フィルターと手動ビューを使用したログベース。<br /><br /> **8** = ストアドプロシージャの実行。<br /><br /> **24** = シリアル化可能なストアドプロシージャの実行。<br /><br /> **32** = ストアドプロシージャ (スキーマのみ)。<br /><br /> **64** = ビュー (スキーマのみ)。<br /><br /> **96** = 集計関数 (スキーマのみ)。<br /><br /> **128** = 関数 (スキーマのみ)。<br /><br /> **257** = ログベースのインデックス付きビュー。<br /><br /> **259** = 手動フィルターを使用したログベースのインデックス付きビュー。<br /><br /> **261** = 手動ビューを使用したログベースのインデックス付きビュー。<br /><br /> **263** = 手動フィルターと手動ビューを使用するログベースのインデックス付きビュー。<br /><br /> **320** = インデックス付きビュー (スキーマのみ)。<br /><br />|  
|**status**|**tinyint**|1つ以上のアーティクルプロパティの [& (ビットごとの and)](../../t-sql/language-elements/bitwise-and-transact-sql.md) の結果にすることができます。<br /><br /> **0x00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0x01** = アーティクルはアクティブです。<br /><br /> **0x08** = insert ステートメントに列名を含めます。<br /><br /> **0x16** = パラメーター化されたステートメントを使用します。<br /><br /> **0x32** = パラメーター化されたステートメントを使用し、insert ステートメントに列名を含めます。|  
|**filter**|**nvarchar (257)**|テーブルを行方向にフィルター選択するために使用されるストアドプロシージャです。 このストアドプロシージャは、FOR REPLICATION 句を使用して作成されている必要があります。|  
|**description**|**nvarchar (255)**|記事の内容を示すエントリ。|  
|**insert_command**|**nvarchar (255)**|Insert をテーブルアーティクルと共にレプリケートするときに使用されるレプリケーションコマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**update_command**|**nvarchar (255)**|テーブルアーティクルで更新をレプリケートするときに使用されるレプリケーションコマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**delete_command**|**nvarchar (255)**|テーブル アーティクルの削除をレプリケートするときに使用されるレプリケーション コマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**creation script path**|**nvarchar (255)**|ターゲットテーブルを作成するために使用されるアーティクルスキーマスクリプトのパスと名前です。|  
|**vertical partition**|**bit**|アーティクルに対して列方向のパーティション分割を有効にするかどうかを指定します。値が **1** の場合は、列方向のパーティション分割が有効になります。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE、または TRUNCATE TABLE の事前作成コマンドです。|  
|**filter_clause**|**ntext**|行方向のフィルター選択を指定する WHERE 句。|  
|**schema_option**|**binary (8)**|指定されたアーティクルのスキーマ生成オプションのビットマップ。 **Schema_option**値の完全な一覧については、「 [transact-sql&#41;&#40;sp_addarticle ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)」を参照してください。|  
|**dest_owner**|**sysname**|対象オブジェクトの所有者の名前。|  
|**source_owner**|**sysname**|ソース オブジェクトの所有者です。|  
|**unqua_source_object**|**sysname**|所有者名の部分を除いたソース オブジェクトの名前です。|  
|**sync_object_owner**|**sysname**|パブリッシュされたアーティクルを定義するビューの所有者です。 .|  
|**unqualified_sync_object**|**sysname**|所有者名を含まない、パブリッシュされたアーティクルを定義するビューの名前。|  
|**filter_owner**|**sysname**|フィルターの所有者。|  
|**unqua_filter**|**sysname**|所有者名の部分を除いたフィルター名です。|  
|**auto_identity_range**|**int**|パブリケーションの作成時に、ID 範囲の自動処理がパブリケーションで有効に設定されたかどうかを示すフラグです。 **1** は、自動 id 範囲が有効になっていることを示します。 **0** は、無効になっていることを示します。|  
|**publisher_identity_range**|**int**|アーティクルの *identityrangemanagementoption* が **auto** に設定されている場合、または **auto_identity_range** が **true**に設定されている場合は、パブリッシャーでの id 範囲の範囲サイズ。|  
|**identity_range**|**bigint**|アーティクルの *identityrangemanagementoption* が **auto** に設定されている場合、または **auto_identity_range** が **true**に設定されている場合は、サブスクライバーでの id 範囲の範囲サイズ。|  
|**threshold**|**bigint**|ディストリビューションエージェントが新しい id 範囲を割り当てるタイミングを示すパーセント値。|  
|**identityrangemanagementoption**|**int**|アーティクルに対して処理される ID 範囲管理を示します。|  
|**fire_triggers_on_snapshot**|**bit**|初期スナップショットが適用されるときに、レプリケートされたユーザートリガーが実行されるかどうかを示します。<br /><br /> **1** = ユーザートリガーが実行されます。<br /><br /> **0** = ユーザートリガーは実行されません。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helparticle** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helparticle**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、 **db_owner**固定データベースロールのメンバー、または現在のパブリケーションのパブリケーションアクセスリストのメンバーだけです。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>参照  
 [アーティクルのプロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
