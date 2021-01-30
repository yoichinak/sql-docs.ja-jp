---
description: sys.fn_cdc_get_min_lsn (Transact-sql)
title: sys.fn_cdc_get_min_lsn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.fn_cdc_get_min_lsn
- fn_cdc_get_min_lsn
- fn_cdc_get_min_lsn_TSQL
- sys.fn_cdc_get_min_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_min_lsn
- sys.fn_cdc_get_min_lsn
ms.assetid: bd49e28a-128b-4f6b-8545-6a2ec3f4afb3
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: f33aa8bfc9f1e2c7160f849bea541dbf70299630
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99194439"
---
# <a name="sysfn_cdc_get_min_lsn-transact-sql"></a>sys.fn_cdc_get_min_lsn (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [Cdc.change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)システムテーブルから、指定されたキャプチャインスタンスの start_lsn 列の値を返します。 この値は、キャプチャ インスタンスの有効期間の下端を表します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_cdc_get_min_lsn ( 'capture_instance_name' )  
```  
  
## <a name="arguments"></a>引数  
 **'** *capture_instance_name* **'**  
 キャプチャ インスタンスの名前を指定します。 *capture_instance_name* は **sysname** です。  
  
## <a name="return-types"></a>戻り値の型  
 **binary(10)**  
  
## <a name="remarks"></a>コメント  
 キャプチャ インスタンスが存在しない場合、または、キャプチャ インスタンスに関連付けられた変更データにアクセスするための権限が呼び出し元にない場合は、0x00000000000000000000 が返されます。  
  
 通常、この関数は、キャプチャインスタンスに関連付けられた変更データキャプチャタイムラインの下端を識別するために使用されます。 また、この関数を使用すると、変更データを要求する前に、クエリ範囲のエンドポイントがキャプチャインスタンスのタイムライン内に収まることを検証することもできます。 変更テーブルでクリーンアップが実行されると、キャプチャ インスタンスの下端が変わるため、こうしたチェックを実行することは重要です。 変更データの要求間の時間が重要である場合、前の変更データ要求の最上位エンドポイントに設定されている低いエンドポイントでも、現在のタイムラインの外部にある可能性があります。  
  
## <a name="permissions"></a>アクセス許可  
 Sysadmin 固定サーバーロールまたは db_owner 固定データベースロールのメンバーシップが必要です。 他のすべてのユーザーに対して、ソーステーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。また、キャプチャインスタンスのゲートロールが定義されている場合は、そのデータベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-returning-the-minimum-lsn-value-for-a-specified-capture-instance"></a>A. 指定したキャプチャ インスタンスの最小 LSN 値を取得する  
 次の例では、データベース内のキャプチャインスタンスの最小 LSN 値を返し `HumanResources_Employee` [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] ます。  
  
```  
USE AdventureWorks2-12;  
GO  
SELECT sys.fn_cdc_get_min_lsn ('HumanResources_Employee')AS min_lsn;  
  
```  
  
### <a name="b-verifying-the-low-endpoint-of-a-query-range"></a>B. クエリ範囲の下端を検証する  
 次の例では、変更データ クエリの下端候補が、キャプチャ インスタンス `sys.fn_cdc_get_min_lsn` の現在のタイムラインに対して有効かどうかを、`HumanResources_Employee` によって返された最小 LSN 値を使って検証します。 この例では、キャプチャインスタンスの前の高エンドポイント LSN が保存されていて、変数を設定できることを前提としてい `@save_to_lsn` ます。 この例では、を `@save_to_lsn` 0x000000000000000000 に設定して、エラー処理セクションを強制的に実行します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @min_lsn binary(10), @from_lsn binary(10),@save_to_lsn binary(10), @to_lsn binary(10);  
-- Sets @save_to_lsn to the previous high endpoint saved from the last change data request.  
SET @save_to_lsn = 0x000000000000000000;  
-- Sets the upper endpoint for the query range to the current maximum LSN.  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
-- Sets the @min_lsn parameter to the current minimum LSN for the capture instance.  
SET @min_lsn = sys.fn_cdc_get_min_lsn ('HumanResources_Employee');  
-- Sets the low endpoint for the query range to the LSN that follows the previous high endpoint.  
SET @from_lsn = sys.fn_cdc_increment_lsn(@save_to_lsn);  
-- Tests to verify the low endpoint is valid for the current capture instance.  
IF (@from_lsn < @min_lsn)  
    BEGIN  
        RAISERROR('Low endpoint of the request interval is invalid.', 16, -1);  
    END  
ELSE  
-- Return the changes occurring within the query range.  
    SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.fn_cdc_get_max_lsn &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md)   
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
