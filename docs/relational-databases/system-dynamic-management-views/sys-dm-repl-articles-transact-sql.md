---
description: sys.dm_repl_articles (Transact-SQL)
title: dm_repl_articles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_articles_TSQL
- dm_repl_articles
- dm_repl_articles_TSQL
- sys.dm_repl_articles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_articles dynamic management function
ms.assetid: 794d514e-bacd-432e-a8ec-3a063a97a37b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ab0bd4b6ff2f862b292f78d9927536c2f9d2be6b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537017"
---
# <a name="sysdm_repl_articles-transact-sql"></a>sys.dm_repl_articles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  レプリケーション トポロジ内のアーティクルとしてパブリッシュされたデータベース オブジェクトに関する情報を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artcache_db_address**|**varbinary (8)**|パブリケーションデータベースのキャッシュされたデータベース構造のメモリ内アドレス。|  
|**artcache_table_address**|**varbinary (8)**|パブリッシュされたテーブルアーティクルのキャッシュされたテーブル構造のメモリ内アドレス。|  
|**artcache_schema_address**|**varbinary (8)**|パブリッシュされたテーブルアーティクルのキャッシュされたアーティクルスキーマ構造のメモリ内アドレス。|  
|**artcache_article_address**|**varbinary (8)**|パブリッシュされたテーブル アーティクルに関する、キャッシュされたアーティクル構造のメモリ内アドレス。|  
|**artid**|**bigint**|このテーブル内の各エントリを一意に識別します。|  
|**artfilter**|**bigint**|アーティクルを行方向へフィルター選択する場合に使用されるストアド プロシージャの ID。|  
|**artobjid**|**bigint**|パブリッシュされたオブジェクトの ID。|  
|**artpubid**|**bigint**|アーティクルが属しているパブリケーションの ID。|  
|**artstatus**|**tinyint**|アーティクルのオプションと状態のビットマスク。これらの値の1つ以上のビットごとの論理和演算を実行できます。<br /><br /> **1** = アーティクルはアクティブです。<br /><br /> **8** = INSERT ステートメントに列名を含めます。<br /><br /> **16** = パラメーター化されたステートメントを使用します。<br /><br /> **24** = INSERT ステートメントに列名を含め、パラメーター化されたステートメントを使用します。<br /><br /> たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの場合、この列の値は17になります。 値0は、アーティクルが非アクティブであり、追加のプロパティが定義されていないことを示します。|  
|**arttype**|**tinyint**|アーティクルの種類:<br /><br /> **1** = ログベースのアーティクル。<br /><br /> **3** = 手動フィルターを使用したログベースのアーティクル。<br /><br /> **5** = 手動ビューを使用したログベースのアーティクル。<br /><br /> **7** = 手動フィルターと手動ビューを使用するログベースのアーティクル。<br /><br /> **8** = ストアドプロシージャの実行。<br /><br /> **24** = シリアル化可能なストアドプロシージャの実行。<br /><br /> **32** = ストアドプロシージャ (スキーマのみ)。<br /><br /> **64** = ビュー (スキーマのみ)。<br /><br /> **128** = 関数 (スキーマのみ)。|  
|**wszArtdesttable**|**nvarchar (514)**|転送先でパブリッシュされたオブジェクトの名前。|  
|**wszArtdesttableowner**|**nvarchar (514)**|パブリッシュ先での、パブリッシュされたオブジェクトの所有者。|  
|**wszArtinscmd**|**nvarchar (510)**|挿入に使用されるコマンドまたはストアド プロシージャ。|  
|**cmdTypeIns**|**int**|Insert ストアドプロシージャの呼び出し構文。これらの値のいずれかを指定できます。<br /><br /> **1** = 呼び出し<br /><br /> **2** = SQL<br /><br /> **3** = なし<br /><br /> **7** = 不明|  
|**wszArtdelcmd**|**nvarchar (510)**|削除に使用されるコマンドまたはストアド プロシージャ。|  
|**cmdTypeDel**|**int**|Delete ストアドプロシージャの呼び出し構文。これらの値のいずれかを指定できます。<br /><br /> **0** = XCALL<br /><br /> **1** = 呼び出し<br /><br /> **2** = SQL<br /><br /> **3** = なし<br /><br /> **7** = 不明|  
|**wszArtupdcmd**|**nvarchar (510)**|更新に使用されるコマンドまたはストアド プロシージャ。|  
|**cmdTypeUpd**|**int**|Update ストアドプロシージャの呼び出し構文。これらの値のいずれかを指定できます。<br /><br /> **0** = XCALL<br /><br /> **1** = 呼び出し<br /><br /> **2** = SQL<br /><br /> **3** = なし<br /><br /> **4** = MCALL<br /><br /> **5** = vcall<br /><br /> **6** = scall<br /><br /> **7** = 不明|  
|**wszArtpartialupdcmd**|**nvarchar (510)**|部分更新に使用されるコマンドまたはストアドプロシージャ。|  
|**cmdTypePartialUpd**|**int**|部分更新ストアド プロシージャの呼び出し構文。次のいずれかになります。<br /><br /> **2** = SQL|  
|**numcol**|**int**|列方向にフィルター選択されたアーティクルのパーティション内の列の数。|  
|**artcmdtype**|**tinyint**|現在レプリケートされているコマンドの種類。次のいずれかになります。<br /><br /> **1** = 挿入<br /><br /> **2** = 削除<br /><br /> **3** = 更新<br /><br /> **4** = UPDATETEXT<br /><br /> **5** = なし<br /><br /> **6** = 内部使用のみ<br /><br /> **7** = 内部使用のみ<br /><br /> **8** = 部分的な更新|  
|**artgeninscmd**|**nvarchar (510)**|アーティクルに含まれる列に基づく INSERT コマンド テンプレート。|  
|**artgendelcmd**|**nvarchar (510)**|DELETE コマンドテンプレート。呼び出し構文に応じて、主キーまたはアーティクルに含まれる列を含めることができます。|  
|**artgenupdcmd**|**nvarchar (510)**|UPDATE コマンドテンプレート。呼び出し構文に応じて、主キー、更新された列、または完全な列リストを含めることができます。|  
|**artpartialupdcmd**|**nvarchar (510)**|部分 UPDATE コマンド テンプレート。主キーと更新された列が含まれます。|  
|**artupdtxtcmd**|**nvarchar (510)**|UPDATETEXT コマンドテンプレート。主キーと更新された列が含まれます。|  
|**artgenins2cmd**|**nvarchar (510)**|同時実行スナップショット処理中にアーティクルを調整するときに使用される INSERT コマンドテンプレート。|  
|**artgendel2cmd**|**nvarchar (510)**|同時実行スナップショット処理中にアーティクルを調整するときに使用される削除コマンドテンプレート。|  
|**fInReconcile**|**tinyint**|同時実行スナップショット処理中にアーティクルが現在調整されているかどうかを示します。|  
|**fPubAllowUpdate**|**tinyint**|パブリケーションがサブスクリプションの更新を許可するかどうかを示します。|  
|**Int文書のオプション**|**bigint**|追加のパブリッシングオプションを指定するビットマップ。ビットごとのオプションの値は次のとおりです。<br /><br /> **0x1** -ピアツーピアレプリケーションに対して有効になります。<br /><br /> **0x2** -ローカル変更のみを発行します。<br /><br /> **0x4** -SQL Server 以外のサブスクライバーに対して有効です。|  
  
## <a name="permissions"></a>アクセス許可  
 **Dm_repl_articles**を呼び出すには、パブリケーションデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>解説  
 情報は、レプリケーションアーティクルキャッシュに現在読み込まれているレプリケートされたデータベースオブジェクトに対してのみ返されます。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [レプリケーション関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

