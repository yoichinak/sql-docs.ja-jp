---
description: sys.fn_cdc_get_column_ordinal (Transact-SQL)
title: sys.fn_cdc_get_column_ordinal (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.fn_cdc_get_column_ordinal
- fn_cdc_get_column_ordinal_TSQL
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal
ms.assetid: 4bb21a57-2b94-4208-8bdf-6a3e2681d881
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 9b778fca1203a7330b1d9f403a31e38ce71433c0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99194458"
---
# <a name="sysfn_cdc_get_column_ordinal-transact-sql"></a>sys.fn_cdc_get_column_ordinal (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたキャプチャインスタンスに関連付けられている [変更テーブル](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) に表示される、指定された列の序数を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_cdc_get_column_ordinal ( 'capture_instance','column_name')  
```  
  
## <a name="arguments"></a>引数  
 **'** *capture_instance* **'**  
 指定された列がキャプチャ対象列として識別されるキャプチャインスタンスの名前を指定します。 *capture_instance* は **sysname** です。  
  
 **'** *column_name* **'**  
 レポート対象の列を示します。 *column_name* は **sysname** です。  
  
## <a name="return-type"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>解説  
 この関数は、変更データキャプチャの更新マスク内でキャプチャされた列の序数位置を識別するために使用されます。 主に、変更データを照会するときに更新マスクから情報を抽出するために、関数 [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) と組み合わせて使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 ソーステーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。 変更データキャプチャコンポーネントのデータベースロールがキャプチャインスタンスに対して指定されている場合は、そのロールのメンバーシップも必要です。  
  
## <a name="examples"></a>例  
 次の例では、`VacationHours` キャプチャ インスタンスの更新マスク内の、`HumanResources_Employee` 列の序数位置を取得します。 さらに、この値を `sys.fn_cdc_is_bit_set` 関数の中で使用し、返された更新マスクから情報を抽出します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10),  @VacationHoursOrdinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @VacationHoursOrdinal = sys.fn_cdc_get_column_ordinal   
    ( 'HumanResources_Employee','VacationHours');  
SELECT *, sys.fn_cdc_is_bit_set(@VacationHoursOrdinal,  
    __$update_mask) as 'VacationHours'  
FROM cdc.fn_cdc_get_net_changes_HumanResources_Employee  
    ( @from_lsn, @to_lsn, 'all with mask');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [変更データ キャプチャの関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.fn_cdc_is_bit_set &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)  
  
  
