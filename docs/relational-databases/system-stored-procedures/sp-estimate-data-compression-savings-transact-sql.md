---
description: sp_estimate_data_compression_savings (Transact-sql)
title: sp_estimate_data_compression_savings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_estimate_data_compression_savings_TSQL
- sp_estimate_data_compression_savings
dev_langs:
- TSQL
helpviewer_keywords:
- compression [SQL Server], estimating
- sp_estimate_data_compression_savings
ms.assetid: 6f6c7150-e788-45e0-9d08-d6c2f4a33729
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4615bc9a30d28224ee3d1ed906a704af923d046d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543500"
---
# <a name="sp_estimate_data_compression_savings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  要求されたオブジェクトの現在のサイズを返し、要求された圧縮状態のオブジェクトサイズを推定します。 圧縮は、テーブル全体またはテーブルの一部について評価できます。 これには、ヒープ、クラスター化インデックス、非クラスター化インデックス、列ストアインデックス、インデックス付きビュー、およびテーブルとインデックスのパーティションが含まれます。 オブジェクトは、行、ページ、列ストア、または列ストアアーカイブの圧縮を使用して圧縮できます。 テーブル、インデックス、またはパーティションが既に圧縮されている場合は、この手順を使用して、テーブル、インデックス、またはパーティションが上げの場合のサイズを見積もることができます。  
  
> [!NOTE]
> 圧縮と**sp_estimate_data_compression_savings**は、のすべてのエディションで使用できるわけではありません [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 要求された圧縮設定を使用した場合のオブジェクト サイズを推定するために、このストアド プロシージャでは、ソース オブジェクトがサンプリングされ、そのデータが tempdb に作成された同等のテーブルとインデックスに読み込まれます。 さらに、tempdb に作成されたテーブルまたはインデックスが要求された設定に圧縮され、圧縮で削減される推定領域が計算されます。  
  
 テーブル、インデックス、またはパーティションの圧縮状態を変更するには、 [ALTER table](../../t-sql/statements/alter-table-transact-sql.md) ステートメントまたは [alter index](../../t-sql/statements/alter-index-transact-sql.md) ステートメントを使用します。 圧縮に関する一般的な情報については、「 [データ圧縮](../../relational-databases/data-compression/data-compression.md)」を参照してください。  
  
> [!NOTE]  
> 既存のデータが断片化されている場合は、インデックスを再構築することで、圧縮を使用しなくてもデータのサイズを削減できる可能性があります。 インデックスの場合、インデックスの再構築中に FILL FACTOR が適用されます。 これによってインデックスのサイズが増える可能性があります。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [ @index_id = ] index_id   
   , [ @partition_number = ] partition_number   
   , [ @data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @schema_name =] '*schema_name*'  
 テーブルまたはインデックス付きビューを含んでいるデータベース スキーマの名前です。 *schema_name* は **sysname**です。 *Schema_name*が NULL の場合は、現在のユーザーの既定のスキーマが使用されます。  
  
 [ @object_name =] '*object_name*'  
 インデックスがあるテーブルまたはインデックス付きビューの名前を指定します。 *object_name* は **sysname** です。  
  
 [ @index_id =] *index_id*  
 インデックスの ID です。 *index_id* は **int**で、次のいずれかの値を指定できます。インデックスの id 番号、NULL、または、 *object_id* がヒープの場合は0です。 ベーステーブルまたはビューのすべてのインデックスに関する情報を返すには、NULL を指定します。 NULL を指定する場合は、 *partition_number*に null も指定する必要があります。  
  
 [ @partition_number =] *partition_number*  
 オブジェクトのパーティション番号です。 *partition_number* は **int**で、次のいずれかの値を指定できます。インデックスまたはヒープのパーティション番号、NULL、または1、非パーティションインデックスまたはヒープ。  
  
 パーティションを指定するには、 [$partition](../../t-sql/functions/partition-transact-sql.md) 関数を指定することもできます。 所有するオブジェクトのすべてのパーティションについて情報を返すには、NULL を指定します。  
  
 [ @data_compression =] '*data_compression*'  
 評価する圧縮の種類を指定します。 *data_compression* 、NONE、ROW、PAGE、列ストア、または COLUMNSTORE_ARCHIVE のいずれかの値を指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 テーブル、インデックス、またはパーティションの現在のサイズと推定サイズを指定するために、次の結果セットが返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|テーブルまたはインデックス付きビューの名前。|  
|schema_name|**sysname**|テーブルまたはインデックス付きビューのスキーマ。|  
|index_id|**int**|インデックスのインデックス ID:<br /><br /> 0 = ヒープ<br /><br /> 1 = クラスター化インデックス<br /><br /> > 1 = 非クラスター化インデックス|  
|partition_number|**int**|パーティション番号。 非パーティションテーブルまたはインデックスの場合は1を返します。|  
|size_with_current_compression_setting (KB)|**bigint**|要求されたテーブル、インデックス、またはパーティションの現在のサイズ。|  
|size_with_requested_compression_setting (KB)|**bigint**|要求された圧縮設定を使用するテーブル、インデックス、またはパーティションの推定サイズ。また、該当する場合は、既存の FILL FACTOR し、断片化が発生していないことを前提としています。|  
|sample_size_with_current_compression_setting (KB)|**bigint**|現在の圧縮設定を使用したサンプルのサイズ。 この列には、断片化も含まれます。|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|要求された圧縮設定を使用して作成されるサンプルのサイズ。また、該当する場合は、既存の FILL FACTOR と断片化はありません。|  
  
## <a name="remarks"></a>解説  
 を使用 `sp_estimate_data_compression_savings` すると、行、ページ、列ストア、または列ストアアーカイブの圧縮に対してテーブルまたはパーティションを有効にした場合に発生する節約量を見積もることができます。 たとえば、行の平均サイズを40% 削減できる場合は、オブジェクトのサイズを40% 小さくすることができます。 これは FILL FACTOR と行サイズに左右されるため、領域を削減できない場合もあります。 たとえば、8000バイトの長さの行があり、そのサイズを40% 削減した場合でも、データページには1つの行だけを収めることができます。 領域は削減されません。  
  
 `sp_estimate_data_compression_savings` を実行してテーブルが増大するという結果が示される場合は、テーブルの多くの行でデータ型の有効桁数がほとんど使用されており、圧縮された形式に必要なわずかなオーバーヘッドが積み重なって、圧縮による削減量を上回ることを意味しています。 このようなまれなケースでは、圧縮を使用しないでください。  
  
 テーブルで圧縮が有効になっている場合は、`sp_estimate_data_compression_savings` を使用して、テーブルが圧縮されていない場合の平均行サイズを推定します。  
  
 この操作中に、テーブルに対して (IS) ロックが取得されます。 (IS) ロックを取得できない場合は、プロシージャがブロックされます。 テーブルは、read committed 分離レベルでスキャンされます。  
  
 要求された圧縮設定が現在の圧縮設定と同じ場合、ストアドプロシージャは、データの断片化のない推定サイズを返し、既存の FILL FACTOR を使用します。  
  
 インデックスまたはパーティション ID が存在しない場合、結果は返されません。  
  
## <a name="permissions"></a>アクセス許可  
 テーブルに対する権限が必要です `SELECT` 。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 SQL Server 2019 より前では、このプロシージャは列ストアインデックスには適用されませんでした。したがって、データ圧縮パラメーターの列ストアと COLUMNSTORE_ARCHIVE は受け入れられませんでした。  SQL Server 2019 以降では、列ストアインデックスは、推定のソースオブジェクトとしても、要求された圧縮の種類としても使用できます。

 > [!IMPORTANT]
 > メモリ最適化された [TempDB メタデータ](../databases/tempdb-database.md#memory-optimized-tempdb-metadata) がで有効になっている場合 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 、一時テーブルでの列ストアインデックスの作成はサポートされていません。 この制限により、メモリ最適化された TempDB メタデータが有効になっている場合、列ストアおよび COLUMNSTORE_ARCHIVE データ圧縮パラメーターで sp_estimate_data_compression_savings はサポートされません。

## <a name="considerations-for-columnstore-indexes"></a>列ストア インデックスに関する考慮事項
 以降で [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] は、 `sp_estimate_compression_savings` 列ストアと列ストアアーカイブの両方の圧縮の推定がサポートされています。 ページと行の圧縮とは異なり、列ストア圧縮をオブジェクトに適用するには、新しい列ストアインデックスを作成する必要があります。 このため、このプロシージャの列ストアと COLUMNSTORE_ARCHIVE オプションを使用する場合、プロシージャに提供されたソースオブジェクトの型によって、圧縮サイズの推定に使用される列ストアインデックスの種類が決まります。 次の表は、 @data_compression パラメーターが列ストアまたは COLUMNSTORE_ARCHIVE に設定されている場合に、各ソースオブジェクトの種類の圧縮節約量を推定するために使用される参照オブジェクトを示しています。

 |ソースオブジェクト|参照オブジェクト|
 |-----------------|---------------|
 |ヒープ|クラスター化列ストア インデックス|
 |クラスター化インデックス|クラスター化列ストア インデックス|
 |非クラスター化インデックス|非クラスター化列ストアインデックス (キー列と、指定された非クラスター化インデックスの付加列を含む)、およびテーブルのパーティション列 (存在する場合)|
 |非クラスター化列ストア インデックス|非クラスター化列ストアインデックス (提供された非クラスター化列ストアインデックスと同じ列を含む)|
 |クラスター化列ストア インデックス|クラスター化列ストア インデックス|

> [!NOTE]  
> 行ストアのソースオブジェクト (クラスター化インデックス、非クラスター化インデックス、またはヒープ) から列ストア圧縮を推定するときに、列ストアインデックスでサポートされていないデータ型を持つ列がソースオブジェクトに存在する場合、sp_estimate_compression_savings はエラーで失敗します。

 同様に、 `@data_compression` パラメーターが、、またはに設定され、 `NONE` `ROW` `PAGE` ソースオブジェクトが列ストアインデックスの場合、使用される参照オブジェクトの概要を次の表に示します。

 |ソースオブジェクト|参照オブジェクト|
 |-----------------|---------------|
 |クラスター化列ストア インデックス|ヒープ|
 |非クラスター化列ストア インデックス|非クラスター化インデックス (キー列として非クラスター化列ストアインデックスに含まれる列と、テーブルのパーティション列 (存在する場合) を付加列として含む)|

> [!NOTE]  
> 列ストアソースオブジェクトから行ストア圧縮 (NONE、ROW、または PAGE) を推定するときに、ソースインデックスに32列を超える列が含まれていないことを確認してください。これは、行ストア (非クラスター化) インデックスでサポートされる制限です。
  
## <a name="examples"></a>例  
 次の例では、`Production.WorkOrderRouting` 圧縮を使用して `ROW` テーブルを圧縮した場合のサイズを推定します。  
  
```sql  
USE AdventureWorks2016;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Unicode 圧縮の実装](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
