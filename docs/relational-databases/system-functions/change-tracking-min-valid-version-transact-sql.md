---
description: CHANGE_TRACKING_MIN_VALID_VERSION (Transact-sql)
title: CHANGE_TRACKING_MIN_VALID_VERSION (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CLEANUP_VERSION
- CHANGE_TRACKING_CLEANUP_VERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGE_TRACKING_MIN_VALID_VERSION
- change tracking [SQL Server], CHANGE_TRACKING_MIN_VALID_VERSION
ms.assetid: 5a43d23f-adcf-4c0b-95ad-07cee03c1f9d
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af42a0f719e490ce32c6f81ee92722a540f1271a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498148"
---
# <a name="change_tracking_min_valid_version-transact-sql"></a>CHANGE_TRACKING_MIN_VALID_VERSION (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)関数を使用するときに、指定したテーブルから変更追跡情報を取得するために有効な、クライアントの最小バージョンを返します。  
    
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CHANGE_TRACKING_MIN_VALID_VERSION ( table_object_id )  
```  
  
## <a name="arguments"></a>引数  
 *table_object_id*  
 テーブルのオブジェクト ID を示します。 *table_object_id* は **int**です。  
  
## <a name="return-type"></a>戻り値の型  
 **bigint**  
  
## <a name="remarks"></a>解説  
 この関数を使用して、CHANGETABLE の *last_sync_version* パラメーターの値を検証します。 *Last_sync_version*がこの関数によって報告された値より小さい場合は、CHANGETABLE への後の呼び出しで返される結果が有効でない可能性があります。  
  
 CHANGE_TRACKING_MIN_VALID_VERSION では、次の情報を使用して戻り値を決定します。  
  
-   テーブルで変更の追跡が有効にされたとき。  
  
-   バックグラウンド クリーンアップ タスクを実行して、データベースに対して指定した保持期間より古い変更追跡情報を削除した日時。  
  
-   テーブルが切り捨てられた場合はです。 これにより、テーブルに関連付けられている変更追跡情報がすべて削除されます。  
  
 次のいずれかの条件に該当する場合、この関数は NULL を返します。  
  
-   データベースで変更の追跡が有効になっていない。  
  
-   指定されたテーブル オブジェクト ID が現在のデータベースで有効でない。  
  
-   オブジェクト ID で指定されたテーブルに対する十分な権限がない。  
  
## <a name="examples"></a>例  
 次の例では、指定されたバージョンが有効なバージョンであるかどうかを判断します。 この例では、テーブルの有効な最小バージョンを取得 `dbo.Employees` し、これを変数の値と比較し `@last_sync_version` ます。 `@last_sync_version` の値が `@min_valid_version` の値より小さい場合、変更された行の一覧は有効ではありません。  
  
> [!NOTE]  
>  通常は、データの同期に使用された最新のバージョン番号が格納されているテーブルまたはその他の場所から値を取得します。  
  
```  
-- The tracked change is tagged with the specified context   
DECLARE @min_valid_version bigint, @last_sync_version bigint;  
  
SET @min_valid_version =   
CHANGE_TRACKING_MIN_VALID_VERSION(OBJECT_ID('dbo.Employees'));  
  
SET @last_sync_version = 11  
IF (@last_sync_version < @min_valid_version)  
-- Error � do not obtain changes  
ELSE  
-- Obtain changes using CHANGETABLE(CHANGES ...)  
```  
  
## <a name="see-also"></a>参照  
 [変更追跡関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
  
