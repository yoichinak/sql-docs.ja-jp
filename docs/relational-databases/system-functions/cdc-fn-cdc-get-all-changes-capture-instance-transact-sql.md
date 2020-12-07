---
description: cdc. fn_cdc_get_all_changes_ &lt; capture_instance &gt;  (transact-sql)
title: cdc. fn_cdc_get_all_changes_ &lt; capture_instance &gt;  (transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_all_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_all_changes_<capture_instance>
ms.assetid: c6bad147-1449-4e20-a42e-b51aed76963c
author: rothja
ms.author: jroth
ms.openlocfilehash: aa461859dcc7d2adc359139e4740ea9272161bf8
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90989945"
---
# <a name="cdcfn_cdc_get_all_changes_ltcapture_instancegt--transact-sql"></a>cdc. fn_cdc_get_all_changes_ &lt; capture_instance &gt;  (transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたログシーケンス番号 (LSN) の範囲内で、ソーステーブルに適用された変更ごとに1行の値を返します。 該当する期間中、1 つのソース行に複数の変更が加えられた場合、返される結果セットには、それぞれの変更が格納されます。 変更データを返すだけでなく、4つのメタデータ列によって、変更を別のデータソースに適用するために必要な情報が提供されます。 行フィルターオプションでは、メタデータ列の内容と、結果セットで返される行が制御されます。 ' All ' 行フィルターオプションを指定した場合は、変更を識別するための行が1つだけになります。 ' All update old ' オプションが指定されている場合、更新操作は2行で表されます。1つは更新前にキャプチャされた列の値を格納し、もう1つは更新後にキャプチャされた列の値を格納します。  
  
 この列挙関数は、ソーステーブルで変更データキャプチャが有効になった時点で作成されます。 関数名は、 **fn_cdc_get_all_changes_**_capture_instance_ 形式で使用されます。ここで *capture_instance* は、ソーステーブルで変更データキャプチャが有効になっている場合に、キャプチャインスタンスに指定された値です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
cdc.fn_cdc_get_all_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all update old  
}  
```  
  
## <a name="arguments"></a>引数  
 *from_lsn*  
 結果セットに含める LSN 範囲の下端を表す LSN 値を指定します。 *from_lsn* は **binary (10)** です。  
  
 結果セットに含まれるのは、 [&#91;capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) 変更テーブルの行のうち、 **__ $ start_lsn** の値が *from_lsn* 以上のものだけです。  
  
 *to_lsn*  
 結果セットに含める LSN 範囲の上端を表す LSN 値を指定します。 *to_lsn* は **binary (10)** です。  
  
 結果セットに含まれるのは、 [&#91;capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) 変更テーブルの行のうち、 **__ start_lsn $** の値が *from_lsn* 以上で *to_lsn* 以下である場合のみです。  
  
 <row_filter_option>:: = {all | update old}  
 メタデータ列の内容と、結果セットで返される行を制御するオプション。  
  
 次のいずれかのオプションを指定できます。  
  
 all  
 指定された LSN 範囲内のすべての変更を返します。 更新操作で生じた変更の場合、更新適用後の新しい値を格納した行だけが返されます。  
  
 すべての更新プログラムが古い  
 指定された LSN 範囲内のすべての変更を返します。 更新操作による変更の場合、このオプションでは、更新前の列の値を含む行と更新後の列の値を含む行の両方が返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|変更のコミット順序を保持する変更に関連付けられているコミット LSN。 同じトランザクションでコミットされた変更は、同じコミット LSN 値を共有します。|  
|**__$seqval**|**binary(10)**|トランザクション内の行への変更を順序付けるために使用されるシーケンス値。|  
|**__$operation**|**int**|変更データの行をターゲットデータソースに適用するために必要なデータ操作言語 (DML) 操作を識別します。 以下のいずれかを指定できます。<br /><br /> 1 = 削除<br /><br /> 2 = 挿入<br /><br /> 3 = 更新 (キャプチャされる列値は更新操作前の値)。 この値が該当するのは、行フィルター オプションに 'all update old' を指定した場合だけです。<br /><br /> 4 = 更新 (キャプチャされた列の値は更新操作後の値)|  
|**__$update_mask**|**varbinary (128)**|キャプチャ インスタンスに対して指定された各キャプチャ対象列に対応するビットを持ったビット マスク。 この値には、 **__ $ operation** が1または2の場合に、定義済みのすべてのビットが1に設定されます。 **__ $ Operation**が3または4の場合、変更された列に対応するビットだけが1に設定されます。|  
|**\<captured source table columns>**|多様|関数によって返されるその他の列は、キャプチャインスタンスの作成時に特定されたキャプチャ対象列です。 キャプチャ対象列リストで列が指定されなかった場合、ソース テーブルのすべての列が返されます。|  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールまたは**db_owner**固定データベースロールのメンバーシップが必要です。 他のすべてのユーザーに対して、ソーステーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。また、キャプチャインスタンスのゲートロールが定義されている場合は、そのデータベースロールのメンバーシップが必要です。 呼び出し元にソースデータを表示するアクセス許可がない場合、関数はエラー 229 ("オブジェクト ' fn_cdc_get_all_changes_... '、データベース ' \<DatabaseName> '、スキーマ ' cdc ') で SELECT 権限が拒否されました。" を返します。  
  
## <a name="remarks"></a>注釈  
 指定した LSN 範囲がキャプチャインスタンスの変更追跡タイムライン内に収まらない場合、関数はエラー 208 ("プロシージャまたは関数 cdc. fn_cdc_get_all_changes に指定された引数の数が不足しています。") を返します。  
  
 **__ $ Operation** = 1 または **__ $ operation** = 3 の場合、データ型**image**、 **text**、および**ntext**の列には常に NULL 値が割り当てられます。 データ型 **varbinary (max)**、 **varchar (max)**、または **nvarchar (max)** の列は、更新中に列が変更されない限り、 **__ $ operation** = 3 の場合は NULL 値が割り当てられます。 **__ $ Operation** = 1 の場合、これらの列には削除時に値が割り当てられます。 キャプチャ インスタンスに含まれる計算列の値は、常に NULL になります。  
  
## <a name="examples"></a>使用例  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]変更データキャプチャのクエリ関数の使用方法を示すいくつかのテンプレートが用意されています。 これらのテンプレートは、の [ **表示** ] メニューで使用でき [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ます。 詳細については、「 [テンプレートエクスプローラー](../../ssms/template/template-explorer.md)」を参照してください。  
  
 この例は、`Enumerate All Changes for Valid Range Template` を示しています。 この例では、関数 `cdc.fn_cdc_get_all_changes_HR_Department` を使用して、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内の HumanResources.Department ソース テーブルに対して定義されているキャプチャ インスタンス `HR_Department` で現在使用できる変更をすべてレポートします。  
  
```  
-- ========  
-- Enumerate All Changes for Valid Range Template  
-- ========  
USE AdventureWorks2012;  
GO  
  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn   = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HR_Department  
  (@from_lsn, @to_lsn, N'all');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [cdc. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [fn_cdc_map_time_to_lsn &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sp_cdc_get_ddl_history &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)   
 [sp_cdc_get_captured_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
