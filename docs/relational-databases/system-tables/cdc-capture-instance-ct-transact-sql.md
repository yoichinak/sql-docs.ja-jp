---
description: cdc。 &lt;capture_instance &gt; _CT (transact-sql)
title: cdc。 &lt;capture_instance &gt; _CT (transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc
- cdc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.<capture_instance>_CT
ms.assetid: 979c8110-3c54-4e76-953c-777194bc9751
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5d0a2dae85606a5e1cb0ffd5f86776e7aae25680
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809785"
---
# <a name="cdcltcapture_instancegt_ct-transact-sql"></a>cdc。 &lt;capture_instance &gt; _CT (transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ソース テーブルに対して変更データ キャプチャを有効にすると作成される変更テーブルです。 ソース テーブルに対して実行された操作が挿入や削除の場合は、各操作について 1 行を返します。ソース テーブルに対して実行された操作が更新の場合は、各操作について 2 行を返します。 ソーステーブルが有効になっているときに変更テーブルの名前が指定されていない場合は、その名前が派生します。 名前の形式は cdc です。*capture_instance*_CT。 *capture_instance* は、ソーステーブルのスキーマ名と *schema_table*形式のソーステーブル名です。 たとえば、 **AdventureWorks**サンプルデータベースのテーブルの**ユーザー**が変更データキャプチャを有効にした場合、派生した変更テーブル名は cdc になり**ます。Person_Address_CT**。  
  
 **システムテーブルに対して直接クエリを実行しない**ことをお勧めします。 代わりに、 [cdc.fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) を実行し、cdc.fn_cdc_get_net_changes_<[capture_instance 関数を>し ](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) ます。  
  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|変更のコミット トランザクションに関連付けられたログ シーケンス番号 (LSN)。<br /><br /> 同じトランザクションでコミットされたすべての変更は、同じコミット LSN を共有します。 たとえば、ソーステーブルに対する削除操作によって2つの行が削除された場合、変更テーブルには、同じ **__ $ start_lsn** 値を持つ2つの行が含まれます。|  
|**__ $ end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> で [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] は、この列は常に NULL です。|  
|**__$seqval**|**binary(10)**|トランザクション内の行の変更を並べ替えるために使用されるシーケンス値。|  
|**__$operation**|**int**|変更に関連付けられているデータ操作言語 (DML) 操作を識別します。 以下のいずれかを指定できます。<br /><br /> 1 = 削除<br /><br /> 2 = 挿入<br /><br /> 3 = 更新 (古い値)<br /><br /> 列データには、更新ステートメントを実行する前の行の値が割り当てられます。<br /><br /> 4 = 更新 (新しい値)<br /><br /> 列データには、更新ステートメントを実行した後の行の値が割り当てられます。|  
|**__$update_mask**|**varbinary (128)**|変更された列を識別する、変更テーブルの列序数に基づくビットマスク。|  
|*\<captured source table columns>*|多様|変更テーブルの残りの列は、キャプチャインスタンスの作成時にキャプチャされた列として識別された、ソーステーブルの列です。 キャプチャ対象列リストで列が指定されなかった場合、ソース テーブルのすべての列がこのテーブルに格納されます。|  
|**__ $ command_id** |**int** |トランザクション内の操作の順序を追跡します。 |  
  
## <a name="remarks"></a>注釈  

列の列は、 `__$command_id` バージョン2012から2016の累積的な更新プログラムで導入されました。 バージョンおよびダウンロードの情報については、 [Microsoft SQL Server データベースに対して変更データキャプチャを有効にした後に、更新された行の変更テーブルの順序が正しく設定さ](https://support.microsoft.com/help/3030352/fix-the-change-table-is-ordered-incorrectly-for-updated-rows-after-you)れ3030352ていないことを確認してください。  詳細については、 [SQL Server 2012、2014、2016の最新の CU にアップグレードした後に、CDC の機能が停止する場合があり](/archive/blogs/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016)ます。

## <a name="captured-column-data-types"></a>キャプチャされた列のデータ型  
 このテーブルに含まれるキャプチャ対象の列のデータ型と値は、対応するソース列と同じですが、次の例外があります。  
  
-   **Timestamp** 列は **binary (8)** として定義されます。  
  
-   **Id** 列は、 **int** または **bigint**として定義されます。  
  
 ただし、これらの列の値は、基になる列の値と同じです。  
  
### <a name="large-object-data-types"></a>ラージ オブジェクト データ型  
 __ $ Operation = 1 また**text**は**image** **ntext** **NULL** \_ \_ $operation = 3 の場合、データ型 image、Text、および ntext の列には常に NULL 値が割り当てられます。 データ型**varbinary (max)**、 **varchar (max)**、または**nvarchar (max)** の列には、 **NULL** \_ \_ 更新中に列が変更されていない限り、$operation が3の場合、NULL 値が割り当てられます。 \_ \_ $Operation = 1 の場合、これらの列には削除時に値が割り当てられます。 キャプチャインスタンスに含まれる計算列の値は、常に **NULL**になります。  
  
 既定では、INSERT、UPDATE、WRITETEXT、または UPDATETEXT の 1 回のステートメントでキャプチャ対象列に追加できる最大サイズは、65,536 バイト (64 KB) です。 大きな LOB データをサポートするためにこのサイズを大きくするには、 [max text repl Size サーバー構成オプション](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md) を使用して、より大きな最大サイズを指定します。 詳細については、「 [max text repl size サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)」を参照してください。  
  
## <a name="data-definition-language-modifications"></a>データ定義言語の変更  
 列の追加や削除など、ソーステーブルに対する DDL の変更は、 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) テーブルに記録されます。 これらの変更は変更テーブルに適用されません。 つまり、変更テーブルの定義は一定のままです。 ソース テーブルには、キャプチャ対象列リストが関連付けられていますが、キャプチャ プロセスで変更テーブルに行を挿入する際、そのリストに存在しない列は無視されます。 キャプチャ対象列リストに指定されていた列が、ソース テーブルから既に削除されていた場合、その列には NULL 値が割り当てられます。  
  
 ソーステーブル内の列のデータ型を変更すると、 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) テーブルにも記録されます。 ただし、この変更によって、変更テーブルの定義が修正されることはありません。 ソース テーブルに対する DDL 変更のログ レコードがキャプチャ プロセスで見つかった場合は、変更テーブルにおけるキャプチャ対象列のデータ型が変更されます。  
  
 ソーステーブル内のキャプチャされた列のデータ型を、データ型のサイズが小さくなるように変更する必要がある場合は、次の手順を実行して、変更テーブル内の同等の列が正常に変更されるようにします。  
  
1.  ソース テーブルで、変更する列の値を、変更後のデータ型に収まるように更新します。 たとえば、データ型を **int** から **smallint**に変更する場合は、値を **smallint** の範囲に収まる-32768 から32767に更新します。  
  
2.  変更テーブルで、同等の列に対して同じ更新操作を実行します。  
  
3.  ソース テーブル側で新しいデータ型を指定します。 データ型の変更は、変更テーブルに正常に反映されます。  

## <a name="data-manipulation-language-modifications"></a>データ操作言語の変更  
 変更データキャプチャが有効になっているソーステーブルに対して挿入、更新、および削除の操作を実行すると、それらの DML 操作のレコードがデータベーストランザクションログに記録されます。 変更データキャプチャプロセスでは、これらの変更に関する情報をトランザクションログから取得し、変更を記録するために1つまたは2つの行を変更テーブルに追加します。 エントリは、ソース テーブルでコミットされたときと同じ順序で変更テーブルに追加されますが、変更テーブルのエントリのコミットは通常 1 つのエントリではなく変更のグループに対して実行される必要があります。  
  
 変更テーブルエントリ内では、 **__ $ start_lsn** 列を使用して、ソーステーブルへの変更に関連付けられているコミット lsn を記録し、 **__ $ seqval 列** を使用してそのトランザクション内の変更を順序付けします。 これらのメタデータ列を一緒に使用して、ソースの変更のコミット順序が維持されるようにすることができます。 キャプチャプロセスではトランザクションログから変更情報を取得するため、変更テーブルのエントリは、対応するソーステーブルの変更と同期して表示されないことに注意する必要があります。 代わりに、キャプチャ プロセスがトランザクション ログから関連の変更エントリを処理した後、対応する変更が非同期で表示されます。  
  
 挿入操作と削除操作については、更新マスクのすべてのビットが設定されます。 更新操作の場合、更新中に変更された列を反映するように、update old 行と update new 行の両方の更新マスクが変更されます。  
  
## <a name="see-also"></a>参照  
 [sys.sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)  
  
