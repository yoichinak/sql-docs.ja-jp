---
description: CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-sql)
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c774b419283ea0d4799ef89c8628095424f169bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498192"
---
# <a name="change_tracking_is_column_in_mask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  CHANGETABLE (CHANGES...) 関数によって返される SYS_CHANGE_COLUMNS 値を解釈します。 これにより、指定した列が SYS_CHANGE_COLUMNS に返された値に含まれているかどうかを、アプリケーションで判断することができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>引数  
 *column_id*  
 チェックする列の ID です。 列 ID を取得するには、 [Columnproperty](../../t-sql/functions/columnproperty-transact-sql.md) 関数を使用します。  
  
 *change_columns*  
 [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)データの SYS_CHANGE_COLUMNS 列のバイナリデータです。  
  
## <a name="return-type"></a>戻り値の型  
 **bit**  
  
## <a name="return-values"></a>戻り値  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK は次の値を返します。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0|指定された列が *change_columns* 一覧にありません。|  
|1|指定された列が *change_columns* 一覧に含まれています。|  
  
## <a name="remarks"></a>解説  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK では、 *column_id*値を検証するためのチェックは実行されません。また、 *column_id*を取得したテーブルから*change_columns*パラメーターが取得されたこともあります。  
  
## <a name="examples"></a>例  
 次の例では、 `Salary` テーブルの列が更新されたかどうかを確認し `Employees` ます。 関数は、 `COLUMNPROPERTY` 列の列 ID を返し `Salary` ます。 `@change_columns`ローカル変数は、データソースとして CHANGETABLE を使用して、クエリの結果に設定する必要があります。  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>参照  
 [変更追跡関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-sql&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
