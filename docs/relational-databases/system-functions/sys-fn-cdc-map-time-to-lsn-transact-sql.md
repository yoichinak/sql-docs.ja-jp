---
description: sys.fn_cdc_map_time_to_lsn (Transact-SQL)
title: fn_cdc_map_time_to_lsn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 638bf2b99069c718e4e84ab0ccc888300a56bc68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427884"
---
# <a name="sysfn_cdc_map_time_to_lsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定された時間について、 [lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)システムテーブルの**start_lsn**列のログシーケンス番号 (LSN) 値を返します。 この関数を使用すると、変更データキャプチャの列挙関数 [cdc. fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) および [cdc. fn_cdc_get_net_changes_ ](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) によって必要とされる LSN 範囲を体系的にマップし、その範囲内のデータ変更を返すことができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>引数  
 **'**<relational_operator>**'** {最大値より大きい \| か、 \| または等しい最小値より大きいか \| 等しい}  
 は、 *tracking_time*値と比較したときに、関連する**tran_end_time**が関連付けられている、 **lsn_time_mapping**テーブル内の個別の LSN 値を識別するために使用されます。  
  
 *relational_operator* は **nvarchar (30)** です。  
  
 *tracking_time*  
 照合する datetime 値を指定します。 *tracking_time* は **datetime**です。  
  
## <a name="return-type"></a>戻り値の型  
 **binary(10)**  
  
## <a name="remarks"></a>解説  
 **Fn_cdc_map_time_lsn**を使用して datetime 範囲を lsn 範囲にマップする方法を理解するには、次のシナリオを検討してください。 変更データを毎日抽出するとします。 つまり、特定の日の午前 0 時までに発生した変更を取得する必要があります。 時間範囲の下限は、前の日の深夜を含めずに最大になります。 上限は、指定された日の深夜を含む最大までの範囲です。 次の例では、 **fn_cdc_map_time_to_lsn** 関数を使用して、この時間ベースの範囲を変更データキャプチャの列挙関数で必要な lsn ベースの範囲に体系的にマップし、その範囲内のすべての変更を返す方法を示しています。  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 関係演算子 ' `smallest greater than` ' は、前日の午前0時より後に発生した変更を制限するために使用されます。 LSN 値が異なる複数のエントリが、 [lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)テーブル内の下限として識別された**tran_end_time**値を共有する場合、関数は、すべてのエントリが含まれていることを確認する最小の lsn を返します。 上限を設定するために、関係演算子 ' ' を使用して、 `largest less than or equal to` 午前0時を含むすべてのエントリを **tran_end_time** 値として範囲に含めます。 LSN 値が異なる複数のエントリが上限として識別された **tran_end_time** 値を共有している場合、関数は、すべてのエントリが含まれていることを保証する最大の lsn を返します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、関数を使用して、 `sys.fn_cdc_map_time_lsn` [lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) テーブルに、 **tran_end_time** 値が午前0時以上の行があるかどうかを確認します。 このクエリを使用すると、たとえば、その日の午前0時にコミットされた変更がキャプチャプロセスによって既に処理されているかどうかを判断し、その日の変更データの抽出を続行できます。  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>参照  
 [cdc. lsn_time_mapping &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [fn_cdc_map_lsn_to_time &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
