---
description: sys.sysindexes (Transact-SQL)
title: sys.sysインデックス (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysindexes
- sysindexes_TSQL
- sys.sysindexes
- sys.sysindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysindexes system table
- sys.sysindexes compatibility view
ms.assetid: f483d89c-35c4-4a08-8f8b-737fd80d13f5
author: rothja
ms.author: jroth
ms.openlocfilehash: 4b78a272e9fa2ec3a0cc3d4418986078ff02f457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88399408"
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベース内のインデックスとテーブルごとに 1 行のデータを格納します。 XML インデックスは、このビューではサポートされていません。 パーティションテーブルとパーティションインデックスは、このビューでは完全にはサポートされていません。代わりに、このカタログ [ビューを使用してください](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|インデックスが属しているテーブルの ID。|  
|**status**|**int**|システム状態情報。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**first**|**binary(6)**|最初のページまたはルートページへのポインター。<br /><br /> **Indid** = 0 の場合は使用されません。<br /><br /> NULL = **indid** > 1 の場合、インデックスはパーティション分割されます。<br /><br /> NULL = **indid** が0または1の場合、テーブルはパーティション分割されます。|  
|**indid**|**smallint**|インデックスの ID:<br /><br /> 0 = ヒープ<br /><br /> 1 = クラスター化インデックス<br /><br /> >1 = 非クラスター化インデックス|  
|**root**|**binary(6)**|**Indid** >= 1**の場合、root はルート**ページへのポインターです。<br /><br /> **Indid** = 0 の場合は使用されません。<br /><br /> NULL = **indid** > 1 の場合、インデックスはパーティション分割されます。<br /><br /> NULL = **indid** が0または1の場合、テーブルはパーティション分割されます。|  
|**minlen**|**smallint**|行の最小サイズ。|  
|**keycnt**|**smallint**|キーの数。|  
|**groupid**|**smallint**|オブジェクトが作成されたファイル グループ ID。<br /><br /> NULL = **indid** > 1 の場合、インデックスはパーティション分割されます。<br /><br /> NULL = **indid** が0または1の場合、テーブルはパーティション分割されます。|  
|**dpages**|**int**|**Indid** = 0 または**indid** = 1 の場合、 **dpages**は使用されているデータページの数です。<br /><br /> **Indid** > 1 の場合、 **dpages**は使用されているインデックスページの数を示します。<br /><br /> 0 = **indid** > 1 の場合、インデックスはパーティション分割されます。<br /><br /> 0 = **indid** が0または1の場合、テーブルはパーティション分割されます。<br /><br /> 行オーバーフローが発生した場合、は正確な結果を生成しません。|  
|**確保**|**int**|**Indid** = 0 または**indid** = 1 の場合、 **reserved**は、すべてのインデックスとテーブルデータに割り当てられたページ数を示します。<br /><br /> **Indid** > 1 の場合、**予約**されるのは、インデックスに割り当てられたページ数です。<br /><br /> 0 = **indid** > 1 の場合、インデックスはパーティション分割されます。<br /><br /> 0 = **indid** が0または1の場合、テーブルはパーティション分割されます。<br /><br /> 行オーバーフローが発生した場合、は正確な結果を生成しません。|  
|**用い**|**int**|**Indid** = 0 または**indid** = 1 の場合は、すべてのインデックスとテーブルデータに使用される合計ページ数が**使用**されます。<br /><br /> **Indid** > 1 の場合は、インデックスに使用されるページ数が**使用さ**れます。<br /><br /> 0 = **indid** > 1 の場合、インデックスはパーティション分割されます。<br /><br /> 0 = **indid** が0または1の場合、テーブルはパーティション分割されます。<br /><br /> 行オーバーフローが発生した場合、は正確な結果を生成しません。|  
|**rowcnt**|**bigint**|**Indid** = 0 および**indid** = 1 に基づくデータレベルの行数。<br /><br /> 0 = **indid** > 1 の場合、インデックスはパーティション分割されます。<br /><br /> 0 = **indid** が0または1の場合、テーブルはパーティション分割されます。|  
|**rowmodctr**|**int**|テーブルの統計情報が前回更新されてから挿入、削除、更新された行の総数。<br /><br /> 0 = **indid** > 1 の場合、インデックスはパーティション分割されます。<br /><br /> 0 = **indid** が0または1の場合、テーブルはパーティション分割されます。<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降では、 **rowmodctr**は以前のバージョンと完全には互換性がありません。 詳細については、「解説」を参照してください。|  
|**reserved3**|**int**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**smallint**|行の最大サイズ|  
|**maxirow**|**smallint**|非リーフインデックス行の最大サイズ。<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降では、 **maxirow**は、以前のバージョンと完全には互換性がありません。|  
|**OrigFillFactor**|**tinyint**|インデックスが作成されたときに使用された元の FILL FACTOR 値。 この値は維持されません。ただし、インデックスを再作成する必要があり、使用された FILL FACTOR 値を記憶していない場合に便利です。|  
|**StatVersion**|**tinyint**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved2**|**int**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**binary(6)**|NULL = インデックスがパーティション分割されています。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**smallint**|インデックスの実装フラグ。<br /><br /> 0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**lockflags**|**smallint**|インデックスのロック粒度を制限するために使用されます。 たとえば、ロック コストを最小限にするには、基本的に読み取り専用の参照テーブルで、テーブル レベルのロックだけを行うように設定します。|  
|**pgmodctr**|**int**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**鍵**|**varbinary(816)**|インデックス キーを構成する列の列 ID の一覧。<br /><br /> NULL を返します。<br /><br /> インデックスキー列を表示するには、 [sys.sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md)を使用します。|  
|**name**|**sysname**|インデックスまたは統計の名前。 **Indid** = 0 の場合は NULL を返します。 アプリケーションを変更して、ヒープ名が NULL であることを確認します。|  
|**statblob**|**image**|統計バイナリ ラージ オブジェクト (BLOB)。<br /><br /> NULL を返します。|  
|**maxlen**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**レコード**|**int**|**Indid = 0**および**indid** = 1 に基づくデータレベルの行数。 **indid** >1 に対して値が繰り返されます。|  
  
## <a name="remarks"></a>解説  
 予約済みとして定義されている列は使用しないでください。  
  
 テーブルまたはインデックスに ROW_OVERFLOW アロケーションユニットのデータが含まれている場合、列 **dpages**、 **reserved**、および **used** では、正確な結果が返されません。 また、各インデックスのページ数は個別に追跡され、ベース テーブル用に集計されることはありません。 ページ数を表示する[には、](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) [allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)カタログビューまたは[dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)動的管理ビューを使用します。  
  
 SQL Server 2000 以前では、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって行レベルの変更カウンターが管理されていました。 現在、こうしたカウンターは列レベルで管理されます。 そのため、 **rowmodctr** 列が計算され、以前のバージョンの結果に似た結果が生成されますが、正確ではありません。  
  
 **Rowmodctr**の値を使用して統計を更新するタイミングを決定する場合は、次の解決策を検討してください。  
  
-   何もしない。 新しい **rowmodctr** 値を使用すると、以前のバージョンの動作が適度に近いため、統計を更新するタイミングを判断する際によく役立ちます。  
  
-   AUTO_UPDATE_STATISTICS を使用します。 詳細については、「 [統計](../../relational-databases/statistics/statistics.md)」を参照してください。  
  
-   時間制限を使用して、統計を更新するタイミングを決定します。 たとえば、1時間ごと、毎日、毎週などです。  
  
-   アプリケーションレベルの情報を使用して、統計を更新するタイミングを決定します。 たとえば、 **id** 列の最大値が1万以上に変更されるたび、または一括挿入操作が実行されるたびに発生します。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
