---
description: dm_repl_schemas (Transact-sql)
title: dm_repl_schemas (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_repl_schemas_TSQL
- dm_repl_schemas
- sys.dm_repl_schemas_TSQL
- sys.dm_repl_schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_schemas dynamic management function
ms.assetid: 6f5fefff-8492-4360-bd5b-a97287367914
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 45ca3d11d1299e2fa308e823f196251066fb6202
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536915"
---
# <a name="sysdm_repl_schemas-transact-sql"></a>dm_repl_schemas (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  レプリケーションでパブリッシュされたテーブル列に関する情報を返します。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artcache_schema_address**|**varbinary (8)**|パブリッシュされたテーブル アーティクルに関する、キャッシュされたスキーマ構造のメモリ内アドレス。|  
|**tabid**|**bigint**|レプリケートされたテーブルの ID。|  
|**indexid**|**smallint**|パブリッシュされたテーブルのクラスター化インデックスの ID。|  
|**idSch**|**bigint**|テーブルスキーマの ID。|  
|**tabschema**|**nvarchar (510)**|テーブルスキーマの名前。|  
|**ccTabschema**|**smallint**|テーブル スキーマの文字長。|  
|**tabname**|**nvarchar (510)**|パブリッシュされたテーブルの名前。|  
|**ccTabname**|**smallint**|パブリッシュされたテーブル名の文字長。|  
|**rowsetid_delete**|**bigint**|削除された行の ID。|  
|**rowsetid_insert**|**bigint**|挿入された行の ID。|  
|**num_pk_cols**|**int**|主キー列の数。|  
|**pcitee**|**バイナリ (8000)**|計算列の評価に使用されるクエリ式の構造へのポインター。|  
|**re_numtextcols**|**int**|レプリケートされたテーブル内のバイナリラージオブジェクト列の数。|  
|**re_schema_lsn_begin**|**バイナリ (8000)**|スキーマ バージョンのログ記録に関する最初のログ シーケンス番号 (LSN)。|  
|**re_schema_lsn_end**|**バイナリ (8000)**|スキーマバージョンのログ記録の終了 LSN。|  
|**re_numcols**|**int**|パブリッシュされた列の数。|  
|**re_colid**|**int**|パブリッシャーの列識別子。|  
|**re_awcName**|**nvarchar (510)**|パブリッシュされた列の名前。|  
|**re_ccName**|**smallint**|列名の文字数。|  
|**re_pk**|**tinyint**|パブリッシュされた列が主キーの一部であるかどうか。|  
|**re_unique**|**tinyint**|パブリッシュされた列が一意のインデックスの一部であるかどうか。|  
|**re_maxlen**|**smallint**|パブリッシュされた列の最大長。|  
|**re_prec**|**tinyint**|パブリッシュされた列の有効桁数。|  
|**re_scale**|**tinyint**|パブリッシュされた列の小数点以下桁数です。|  
|**re_collatid**|**bigint**|パブリッシュされた列の照合順序 ID。|  
|**re_xvtype**|**smallint**|パブリッシュされた列の型。|  
|**re_offset**|**smallint**|パブリッシュされた列のオフセット。|  
|**re_bitpos**|**tinyint**|パブリッシュされた列のバイトベクター内のビット位置。|  
|**re_fNullable**|**tinyint**|パブリッシュされた列が NULL 値をサポートするかどうかを指定します。|  
|**re_fAnsiTrim**|**tinyint**|パブリッシュされた列で ANSI trim を使用するかどうかを指定します。|  
|**re_computed**|**smallint**|パブリッシュされた列が計算列であるかどうかを指定します。|  
|**se_rowsetid**|**bigint**|行セットの ID。|  
|**se_schema_lsn_begin**|**バイナリ (8000)**|スキーマ バージョンのログ記録に関する最初の LSN。|  
|**se_schema_lsn_end**|**バイナリ (8000)**|スキーマバージョンのログ記録の終了 LSN。|  
|**se_numcols**|**int**|列の数。|  
|**se_colid**|**int**|サブスクライバーでの列の ID。|  
|**se_maxlen**|**smallint**|列の最大長。|  
|**se_prec**|**tinyint**|列の有効桁数。|  
|**se_scale**|**tinyint**|列の小数点以下桁数。|  
|**se_collatid**|**bigint**|列の照合順序 ID。|  
|**se_xvtype**|**smallint**|列の型。|  
|**se_offset**|**smallint**|列のオフセット。|  
|**se_bitpos**|**tinyint**|バイトベクター内の列のビット位置。|  
|**se_fNullable**|**tinyint**|列が NULL 値をサポートするかどうかを指定します。|  
|**se_fAnsiTrim**|**tinyint**|列で ANSI trim を使用するかどうかを指定します。|  
|**se_computed**|**smallint**|列が計算列であるかどうかを指定します。|  
|**se_nullBitInLeafRows**|**int**|列の値が NULL かどうかを指定します。|  
  
## <a name="permissions"></a>アクセス許可  
 **Dm_repl_schemas**を呼び出すには、パブリケーションデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>解説  
 情報は、レプリケーションアーティクルキャッシュに現在読み込まれているレプリケートされたデータベースオブジェクトに対してのみ返されます。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [レプリケーション関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

