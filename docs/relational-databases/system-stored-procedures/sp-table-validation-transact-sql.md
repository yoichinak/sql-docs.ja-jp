---
description: sp_table_validation (Transact-sql)
title: sp_table_validation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 88ee13025153fff3018fadfa8d64becf7a534303
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545933"
---
# <a name="sp_table_validation-transact-sql"></a>sp_table_validation (Transact-sql)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  テーブルまたはインデックス付きビューの行数またはチェックサム情報を返すか、あるいは提供された行数またはチェックサム情報を指定のテーブルまたはインデックス付きビューと比較します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行され、サブスクライバー側でサブスクリプションデータベースに対して実行されます。 *Oracle パブリッシャーではサポートされていません*。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_table_validation [ @table = ] 'table'  
    [ , [ @expected_rowcount = ] type_of_check_requested OUTPUT]  
    [ , [ @expected_checksum = ] expected_checksum OUTPUT]  
    [ , [ @rowcount_only = ] rowcount_only ]  
    [ , [ @owner = ] 'owner' ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @table_name = ] table_name ]  
    [ , [ @column_list = ] 'column_list' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table = ] 'table'` テーブルの名前を指定します。 *table* の **sysname**,、既定値はありません。  
  
`[ @expected_rowcount = ] expected_rowcountOUTPUT` テーブル内の予想行数を返すかどうかを指定します。 *expected_rowcount* は **int**,、既定値は NULL です。 NULL の場合、実際の行数は出力パラメーターとして返されます。 値が提供されると、その値は実際の行数と照合され、違いがあるかどうかが識別されます。  
  
`[ @expected_checksum = ] expected_checksumOUTPUT` テーブルに対して予期されるチェックサムを返すかどうかを指定します。 *expected_checksum* は **numeric**で、既定値は NULL です。 NULL の場合、実際のチェックサムは出力パラメーターとして返されます。 値が指定されている場合は、その値が実際のチェックサムに照らしてチェックされ、相違点が特定されます。  
  
`[ @rowcount_only = ] type_of_check_requested` 実行するチェックサムまたは行数の種類を指定します。 *type_of_check_requested* は **smallint**,、既定値は **1**です。  
  
 **0**の場合は、rowcount と7.0 と互換性のあるチェックサムを実行し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 **1**の場合は、行数チェックのみを実行します。  
  
 **2**の場合は、行数とバイナリチェックサムを実行します。  
  
`[ @owner = ] 'owner'` テーブルの所有者の名前を指定します。 *owner* は **sysname**,、既定値は NULL です。  
  
`[ @full_or_fast = ] full_or_fast` 行数を計算するために使用されるメソッドです。 *full_or_fast* は **tinyint**,、既定値は **2**,、これらの値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|COUNT(*) を使用してフル カウントします。|  
|**1**|Sysindexes から高速にカウントさ **れ**ます。 **Sysindexes**での行のカウントは、実際のテーブルの行をカウントするよりもはるかに高速です。 ただし、 **sysindexes** は遅延更新されるため、行数が正確でない場合があります。|  
|**2** (既定値)|最初に高速カウントを試み、条件高速カウントを行います。 Fast メソッドが相違点を示している場合、は完全なメソッドに戻ります。 *Expected_rowcount*が NULL で、ストアドプロシージャを使用して値を取得している場合は、常に完全なカウント (*) が使用されます。|  
  
`[ @shutdown_agent = ] shutdown_agent` ディストリビューションエージェントが **sp_table_validation**を実行している場合は、検証の完了後すぐにディストリビューションエージェントをシャットダウンするかどうかを指定します。 *shutdown_agent* は **ビット**,、既定値は **0**です。 **0**の場合、レプリケーションエージェントはシャットダウンされません。 **1**の場合、エラー20578が発生し、レプリケーションエージェントはシャットダウンするように通知されます。 このパラメーターは、ユーザーが直接 **sp_table_validation** を実行する場合は無視されます。  
  
`[ @table_name = ] table_name` 出力メッセージに使用されるビューのテーブル名を指定します。 *table_name*は**sysname**で、既定値は** \@ table**です。  
  
`[ @column_list = ] 'column_list'` チェックサム関数で使用する列の一覧です。 *column_list* は **nvarchar (4000)**,、既定値は NULL です。 マージ アーティクルを検証する場合は、計算列とタイムスタンプ列を除く列リストを指定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 チェックサムの検証を実行し、予期されるチェックサムがテーブルのチェックサムと等しい場合、 **sp_table_validation** は、テーブルがチェックサムの検証に合格したことを示すメッセージを返します。 それ以外の場合は、テーブルが同期されていない可能性があるというメッセージを返し、予想される行数と実際の行数との差を報告します。  
  
 行数の検証を実行し、予想される行数がテーブルの数と等しい場合、 **sp_table_validation** はテーブルが行数の検証に合格したというメッセージを返します。 それ以外の場合は、テーブルが同期されていない可能性があるというメッセージを返し、予想される行数と実際の行数との差を報告します。  
  
## <a name="remarks"></a>解説  
 **sp_table_validation** は、すべての種類のレプリケーションで使用されます。 **sp_table_validation** は、Oracle パブリッシャーではサポートされていません。  
  
 Checksum は、ページ上の行イメージ全体で32ビット巡回冗長検査 (CRC) を計算します。 チェックサムは、列を選択して検査するわけではなく、テーブルのビューや列方向のパーティションで動作できません。 また、チェックサムでは、 **text** 列と **image** 列の内容がスキップされます (仕様)。  
  
 チェックサムを実行する場合、テーブルの構造は、2つのサーバー間で同一である必要があります。つまり、同じ順序、同じデータ型と長さ、および同じ NULL/NOT NULL 条件で同じ列がテーブルに存在している必要があります。 たとえば、パブリッシャーが CREATE TABLE を行った場合、列を追加するための ALTER TABLE ですが、サブスクライバー側で適用されるスクリプトは単純な CREATE table ですが、構造は同じではありません。 2つのテーブルの構造が同一でない場合は、 [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) を調べて、各テーブル内のオフセットが同じであることを確認します。  
  
 文字モードの **bcp** を使用した場合、浮動小数点値によってチェックサムの違いが生じる可能性があります。これは、パブリケーションに以外のサブスクライバーが含まれている場合に発生し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これは、文字モード間で変換を実行するときの、わずかではあるが避けられない有効桁数の違いに基づきます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_table_validation**を実行するには、検証対象のテーブルに対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [チェックサム &#40;Transact-sql&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
