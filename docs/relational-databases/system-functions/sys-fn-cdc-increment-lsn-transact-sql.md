---
description: sys.fn_cdc_increment_lsn (Transact-sql)
title: sys.fn_cdc_increment_lsn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn
- fn_cdc_increment_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_increment_lsn
- sys.fn_cdc_increment_lsn
ms.assetid: e53b6703-358b-4c9a-912a-8f7c7331069b
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: ee5d44cbe53d31609a454eb5acbed52a53ae194e
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98099681"
---
# <a name="sysfn_cdc_increment_lsn-transact-sql"></a>sys.fn_cdc_increment_lsn (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定された LSN の直後のログ シーケンス番号 (LSN) を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_cdc_increment_lsn ( lsn_value )  
```  
  
## <a name="arguments"></a>引数  
 *lsn_value*  
 LSN 値を指定します。 *lsn_value* は **binary (10)** です。  
  
## <a name="return-type"></a>戻り値の型  
 **binary(10)**  
  
## <a name="remarks"></a>解説  
 関数によって返される LSN 値は、常に指定された値より大きくなり、2つの値の間に LSN 値は存在しません。  
  
 時間の経過と共に変更データのストリームを体系的にクエリするには、クエリで返される変更をバインドする新しいクエリ間隔を指定するたびに、クエリ関数呼び出しを定期的に繰り返すことができます。 データが失われないようにするために、前のクエリの上限を使用して、その後のクエリの下限を生成することがよくあります。 クエリ間隔は終了間隔であるため、新しい下限は前の上限よりも大きくする必要がありますが、この値と古い上限の間にある LSN 値が変更されていないことを確認するのに十分な大きさにする必要があります。 sys.fn_cdc_increment_lsn 関数は、このような値を取得するために使用します。  
  
## <a name="permissions"></a>アクセス許可  
 public データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、前回のクエリ時に保存した上限を `sys.fn_cdc_increment_lsn` 変数に格納し、それを `@save_to_lsn` 関数に渡すことによって、変更データ キャプチャ クエリに使用する新しい下限値を取得しています。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10), @save_to_lsn binary(10);  
SET @save_to_lsn = <previous_upper_bound_value>;  
SET @from_lsn = sys.fn_cdc_increment_lsn(@save_to_lsn);  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * from cdc.fn_cdc_get_all_changes_HumanResources_Employee( @from_lsn, @to_lsn, 'all' );  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.fn_cdc_decrement_lsn &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
