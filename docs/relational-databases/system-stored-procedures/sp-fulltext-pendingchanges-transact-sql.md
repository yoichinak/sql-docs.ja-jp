---
description: sp_fulltext_pendingchanges (Transact-sql)
title: sp_fulltext_pendingchanges (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6befa1abf7f427ab59c851fac9e51933ecc97bb7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538907"
---
# <a name="sp_fulltext_pendingchanges-transact-sql"></a>sp_fulltext_pendingchanges (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  変更の追跡を使用している指定されたテーブルについて、保留中の挿入、更新、削除などの未処理の変更を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_pendingchanges table_id  
```  
  
## <a name="arguments"></a>引数  
 *table_id*  
 テーブルの ID。 テーブルでフルテキストインデックスが作成されていない場合、またはテーブルで変更の追跡が有効になっていない場合は、エラーが返されます。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**キー**|*|指定したテーブルからのフルテキスト キー値。|  
|**DocId**|**bigint**|キー値に対応する内部ドキュメント識別子 (DocId) 列。|  
|**状態**|**int**|0 = 行は、フルテキストインデックスから削除されます。<br /><br /> 1 = 行にはフルテキスト インデックスが作成されます。<br /><br /> 2 = 行は最新です。<br /><br /> -1 = 行は遷移中 (バッチ処理されているがコミットされていない) 状態またはエラー状態です。|  
|**DocState**|**tinyint**|内部ドキュメント識別子 (Docld) のマップ ステータス列の行ダンプ。|  
  
 <sup>* Key のデータ型は、ベース テーブルのフルテキスト キー列のデータ型と同じです。</sup>  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="remarks"></a>解説  
 未処理の変更がない場合、空の行セットが返されます。  
  
 フルテキスト検索クエリでは、 **Status** 値が0の行は返されません。 これは、行がベーステーブルから削除され、フルテキストインデックスから削除されるのを待機しているためです。  
  
 特定のテーブルに対して保留中の変更の数を確認するには、OBJECTPROPERTYEX 関数の **TableFullTextPendingChanges** プロパティを使用します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のフルテキスト検索およびセマンティック検索ストアドプロシージャ ](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
