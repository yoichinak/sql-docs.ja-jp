---
description: sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL)
title: sp_estimated_rowsize_reduction_for_vardecimal (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- sp_estimated_rowsize_reduction_for_vardecimal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- decimal data type, compressing
- numeric data type, compressing
- estimate decimal compression
- table compression [SQL Server]
ms.assetid: 0fe45983-f9f2-4c7f-938a-0fd96e1cbe8d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f4ab6fbd33edef26f9cf1d37daf6688a68d8d5eb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89527922"
---
# <a name="sp_estimated_rowsize_reduction_for_vardecimal-transact-sql"></a>sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  テーブルで vardecimal ストレージ形式を有効にした場合に、行の平均サイズの減少を推定します。 この数値を使用して、テーブル サイズ全体の削減量を見積もることができます。 統計サンプリングは、行サイズの平均減少を計算するために使用されます。これは、推定値としてのみ考慮されます。 vardecimal ストレージ形式を有効にした後、まれに行サイズが増加する場合があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]代わりに、行の圧縮とページの圧縮を使用してください。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。 テーブルとインデックスのサイズに対する圧縮効果については、「 [transact-sql&#41;&#40;sp_estimate_data_compression_savings ](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_estimated_rowsize_reduction_for_vardecimal [ [ @table_name = ] 'table'] [;]  
```  
  
## <a name="arguments"></a>引数  
`[ @table = ] 'table'` ストレージ形式を変更するテーブルの3部構成の名前を指定します。 *テーブル* は **nvarchar (776)** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の結果セットは、テーブルの現在のサイズと推定サイズの情報を提供するために返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**avg_rowlen_fixed_format**|**decimal (12, 2)**|固定10進ストレージ形式の行の長さを表します。|  
|**avg_rowlen_vardecimal_format**|**decimal (12, 2)**|Vardecimal ストレージ形式が使用されている場合の平均行サイズを表します。|  
|**row_count**|**int**|テーブル内の行の数。|  
  
## <a name="remarks"></a>解説  
 テーブルで vardecimal ストレージ形式を有効にした場合の結果の節約量を見積もるには、 **sp_estimated_rowsize_reduction_for_vardecimal** を使用します。 たとえば、行の平均サイズを40% に減らすことができる場合は、テーブルのサイズを40% 小さくすることができます。 ただし FILL FACTOR と行サイズによっては、テーブル領域を削減できない場合もあります。 たとえば、長さ 8,000 バイトの行があり、そのサイズを 40% を削減したとしても、データ ページに収まるのは 1 行のみであることに変わりはないので、領域は削減されません。  
  
 **Sp_estimated_rowsize_reduction_for_vardecimal**の結果によってテーブルが大きくなることが示された場合、テーブルの多くの行では decimal データ型の有効桁数がほぼすべて使用されます。また、vardecimal ストレージ形式に必要な少量のオーバーヘッドの追加は、vardecimal ストレージ形式の節約よりも大きくなります。 このようなまれなケースでは、vardecimal ストレージ形式を有効にしないでください。  
  
 テーブルで vardecimal ストレージ形式が有効になっている場合は、 **sp_estimated_rowsize_reduction_for_vardecimal** を使用して、vardecimal ストレージ形式が無効になっている場合に行の平均サイズを見積もることができます。  
  
## <a name="permissions"></a>アクセス許可  
 テーブルに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、 `Production.WorkOrderRouting` データベース内のテーブルが圧縮されている場合に行サイズの削減を推定し `AdventureWorks2012` ます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimated_rowsize_reduction_for_vardecimal 'Production.WorkOrderRouting' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_db_vardecimal_storage_format &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
