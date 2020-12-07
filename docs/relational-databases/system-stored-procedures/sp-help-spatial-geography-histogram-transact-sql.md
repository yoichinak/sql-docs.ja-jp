---
description: sp_help_spatial_geography_histogram (Transact-sql)
title: sp_help_spatial_geography_histogram (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_histogram_TSQL
- sp_help_spatial_geography_histogram
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_histogram
ms.assetid: 5c5bd319-055d-4cd6-8c5a-06354cc056cc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0c7368b8991fe442cab30b724532e8899502e18f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809393"
---
# <a name="sp_help_spatial_geography_histogram-transact-sql"></a>sp_help_spatial_geography_histogram (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  空間インデックスのグリッドパラメーターのキー付けを容易にします。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_spatial_geography_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @sample = ] 'tablesample' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tabname = ] 'tabname'` 空間インデックスが指定されているテーブルの修飾名または修飾され名を指定します。  
  
 引用符は、修飾されたテーブルが指定されている場合にのみ必要です。 データベース名を含む完全修飾名を指定する場合は、データベース名を現在のデータベースの名前にする必要があります。 *tabname* は **sysname**,、既定値はありません。  
  
`[ @colname = ] 'columnname'` 指定された空間列の名前を指定します。 *columnname* は **sysname**,、既定値はありません。  
  
`[ @resolution = ] 'resolution'` 境界ボックスの解像度です。 有効な値は 10 ～ 5000 です。 *解決策* は **tinyint**,、既定値はありません。  
  
`[ @sample = ] 'sample'` 使用するテーブルの割合を示します。 有効な値は 0 ~ 100 です。 *tablesample* は **float**です。 既定値は100です。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 テーブル値が返されます。 次のグリッドでは、テーブルの列の内容について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|各セルの一意の ID を表します。開始カウントは1です。|  
|**cell**|**geography**|それぞれのセルを表す四角形です。 セルの形は、空間インデックス作成用に使用されたセルの形と同じです。|  
|**row_count**|**bigint**|セルをタッチまたは格納している空間オブジェクトの数を示します。|  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、 **public** ロールのメンバーである必要があります。 サーバーとオブジェクトに対する読み取りアクセス権限が必要です。  
  
## <a name="remarks"></a>注釈  
 SSMS 空間タブでは、結果がグラフィカルに表示されます。 空間ウィンドウに対して結果にクエリを実行すると、結果項目の概数を取得できます。  
  
> [!NOTE]  
>  テーブル内のオブジェクトは複数のセルに対応している場合があるため、テーブル内のセルの合計が実際のオブジェクトの数よりも大きくなる可能性があります。  
  
 **Geography**型の境界ボックスは、地球全体です。  
  
## <a name="examples"></a>例  
 次の例では、データベースのテーブルで  **sp_help_spatial_geography_histogram** を呼び出し `Person.Address` [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] ます。  
  
```  
EXEC sp_help_spatial_geography_histogram @tabname = Person.Address, @colname = SpatialLocation, @resolution = 64, @sample = 30;  
```  
  
## <a name="see-also"></a>参照  
 [空間インデックスストアドプロシージャ &#40;Transact-sql&#41;](./spatial-index-stored-procedures-arguments-and-properties.md)  
  
