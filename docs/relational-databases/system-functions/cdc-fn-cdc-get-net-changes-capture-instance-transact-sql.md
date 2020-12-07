---
description: cdc. fn_cdc_get_net_changes_ &lt; capture_instance &gt; (transact-sql)
title: cdc. fn_cdc_get_net_changes_ &lt; capture_instance &gt; (transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_net_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_net_changes_<capture_instance>
ms.assetid: 43ab0d1b-ead4-471c-85f3-f6c4b9372aab
author: rothja
ms.author: jroth
ms.openlocfilehash: 731effd8310521308f9097323d10fcc57bcb9921
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498221"
---
# <a name="cdcfn_cdc_get_net_changes_ltcapture_instancegt-transact-sql"></a>cdc. fn_cdc_get_net_changes_ &lt; capture_instance &gt; (transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたログシーケンス番号 (LSN) の範囲内で変更されたソース行ごとに1つの差分変更行を返します。  
  
 **LSN とは何ですか。** [SQL Server トランザクションログ](../logs/the-transaction-log-sql-server.md)のすべてのレコードは、ログシーケンス番号 (LSN) によって一意に識別されます。 Lsn は、LSN2 が LSN1 より大きい場合に、LSN2 によって参照されるログレコードによって示される変更が、ログレコード LSN によって記述された変更の **後** に発生するように並べ替えられます。  
  
 重要なイベントが発生したログレコードの LSN は、正しい復元シーケンスを構築するのに役立ちます。 Lsn は順序付けられているため、等しいかどうかを比較できます (つまり、 \<, > =、 \<=, > =)。 このような比較は、復元シーケンスを構築するときに役立ちます。  
  
 LSN 範囲内でソース行に複数の変更がある場合、行の最終的な内容を反映した1行が、次に示す列挙関数によって返されます。 たとえば、トランザクションがソーステーブルに行を挿入し、LSN 範囲内の後続のトランザクションがその行の1つ以上の列を更新する場合、関数は、更新された列の値を含む **1** 行だけを返します。  
  
 この列挙関数は、ソーステーブルで変更データキャプチャが有効になっていて、net tracking が指定されている場合に作成されます。 差分の追跡を有効にするには、ソーステーブルに主キーまたは一意のインデックスが必要です。 関数名は、fn_cdc_get_net_changes_*capture_instance*の形式で使用されます。ここで *capture_instance* は、ソーステーブルで変更データキャプチャが有効にされたときにキャプチャインスタンスに対して指定された値です。 詳細については、「 [sys. sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
cdc.fn_cdc_get_net_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all with mask  
 | all with merge  
}  
```  
  
## <a name="arguments"></a>引数  
 *from_lsn*  
 結果セットに含める LSN 範囲の下端を表す LSN です。 *from_lsn* は **binary (10)** です。  
  
 結果セットに含まれるのは、 [&#91;capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) 変更テーブルの行のうち、__ $ start_lsn の値が *from_lsn* 以上のものだけです。  
  
 *to_lsn*  
 結果セットに含める LSN 範囲の上端を表す LSN を指定します。 *to_lsn* は **binary (10)** です。  
  
 結果セットに含まれるのは、 [&#91;capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)変更テーブルの行のうち、__ start_lsn $ の*値が* *from_lsn 以下 to_lsn または*等しい場合のみです。  
  
 *<row_filter_option>* :: = {all | mask | all with merge}  
 メタデータ列の内容と、結果セットで返される行を制御するオプション。 次のいずれかのオプションを指定できます。  
  
 all  
 行に対する最終的な変更の LSN と、メタデータ列 __ $ start_lsn および $operation の行を適用するために必要な操作を返し \_ \_ ます。 _Mask 列 \_ \_ $update は常に NULL です。  
  
 すべてマスク付き  
 行に対する最終的な変更の LSN と、メタデータ列 __ $ start_lsn および $operation の行を適用するために必要な操作を返し \_ \_ ます。 また、更新操作によってが返される場合 ( \_ \_ $operation = 4)、更新で変更されたキャプチャ対象列は $update _mask で返される値でマークされ \_ \_ ます。  
  
 merge を使用したすべて  
 行に対する最終的な変更の LSN が、メタデータ列 __$start_lsn に返されます。 列 \_ \_ $operation は2つの値のいずれかになります。削除の場合は1、変更を適用するために必要な操作が挿入または更新のいずれかであることを示す5。 _Mask 列 \_ \_ $update は常に NULL です。  
  
 特定の変更に対する正確な操作を決定するロジックによってクエリの複雑さが増すため、このオプションは、変更データを適用するために必要な操作が挿入または更新のいずれかであることを示すのに十分な場合に、クエリのパフォーマンスを向上させるように設計されています。 このオプションは、環境など、マージ操作を直接利用できるターゲット環境で最も魅力的です [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|__$start_lsn|**binary(10)**|変更のコミット トランザクションに関連付けられた LSN。<br /><br /> 同じトランザクションでコミットされたすべての変更は、同じコミット LSN を共有します。 たとえば、ソーステーブルの更新操作によって2つの行の2つの列が変更された場合、変更テーブルには、それぞれ同じ __ $ start_lsnvalue を持つ4つの行が含まれます。|  
|__$operation|**int**|変更データの行をターゲットデータソースに適用するために必要なデータ操作言語 (DML) 操作を識別します。<br /><br /> row_filter_option パラメーターの値が all または all with mask である場合、この列の値には、次のいずれかの値を指定できます。<br /><br /> 1 = 削除<br /><br /> 2 = 挿入<br /><br /> 4 = 更新<br /><br /> row_filter_option パラメーターの値が all with merge である場合、この列の値には、次のいずれかの値を指定できます。<br /><br /> 1 = 削除|  
|__$update_mask|**varbinary (128)**|キャプチャ インスタンスに対して指定された各キャプチャ対象列に対応するビットを持ったビット マスク。 この値には、__ $ operation が1または2の場合に、定義済みのすべてのビットが1に設定されます。 \_ \_ $Operation が3または4の場合、変更された列に対応するビットだけが1に設定されます。|  
|*\<captured source table columns>*|多様|この関数によって返されるその他の列は、ソース テーブルの列のうち、キャプチャ インスタンスの作成時にキャプチャ対象として指定された列です。 キャプチャ対象列リストで列が指定されなかった場合、ソース テーブルのすべての列が返されます。|  
  
## <a name="permissions"></a>アクセス許可  
 Sysadmin 固定サーバーロールまたは db_owner 固定データベースロールのメンバーシップが必要です。 他のすべてのユーザーに対して、ソーステーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。また、キャプチャインスタンスのゲートロールが定義されている場合は、そのデータベースロールのメンバーシップが必要です。 呼び出し元にソースデータを表示するアクセス許可がない場合、関数はエラー 208 (無効なオブジェクト名) を返します。  
  
## <a name="remarks"></a>解説  
 指定した LSN 範囲が、キャプチャ インスタンスの変更追跡時間外に該当した場合、エラー 208 (無効なオブジェクト名) が返されます。

 行の一意の識別子を変更すると、fn_cdc_get_net_changes によって最初の更新コマンドが削除され、その後 INSERT コマンドが表示されるようになります。  この動作は、変更前と変更後の両方のキーを追跡するために必要です。
  
## <a name="examples"></a>例  
 次の例では、関数を使用して、 `cdc.fn_cdc_get_net_changes_HR_Department` 特定の時間間隔中にソーステーブルに対して行われた差分変更を報告し `HumanResources.Department` ます。  
  
 まず、関数を使用して、 `GETDATE` 時間間隔の開始をマークします。 ソース テーブルに対して複数の DML ステートメントを適用した後、再び `GETDATE` 関数を呼び出して期間の終わりを指定します。 次に、関数 [sys. fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) を使用して、lsn 値で制限された変更データキャプチャのクエリ範囲に時間間隔をマップします。 最後に、`cdc.fn_cdc_get_net_changes_HR_Department` 関数を呼び出して、該当期間中に行われたソース テーブルへの差分変更を取得します。 挿入され、削除された行は、関数によって返される結果セットには表示されないことに注意してください。 たとえ行を追加しても、同じ期間内に削除されれば、その期間におけるソース テーブルへの差分変更とはならないためです。 この例を実行する前に、最初に例 B を実行する必要があり [ます sys. sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)です。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @begin_time datetime, @end_time datetime, @from_lsn binary(10), @to_lsn binary(10);  
-- Obtain the beginning of the time interval.  
SET @begin_time = GETDATE() -1;  
-- DML statements to produce changes in the HumanResources.Department table.  
INSERT INTO HumanResources.Department (Name, GroupName)  
VALUES (N'MyDept', N'MyNewGroup');  
  
UPDATE HumanResources.Department  
SET GroupName = N'Resource Control'  
WHERE GroupName = N'Inventory Management';  
  
DELETE FROM HumanResources.Department  
WHERE Name = N'MyDept';  
  
-- Obtain the end of the time interval.  
SET @end_time = GETDATE();  
-- Map the time interval to a change data capture query range.  
SET @from_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than or equal', @begin_time);  
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);  
  
-- Return the net changes occurring within the query window.  
SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@from_lsn, @to_lsn, 'all');  
```  
  
## <a name="see-also"></a>参照  
 [cdc. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [fn_cdc_map_time_to_lsn &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
