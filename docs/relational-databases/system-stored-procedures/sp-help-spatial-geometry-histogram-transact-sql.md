---
description: sp_help_spatial_geometry_histogram (Transact-SQL)
title: sp_help_spatial_geometry_histogram (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_histogram
- sp_help_spatial_geometry_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_histogram
ms.assetid: 036aaf61-df3e-40f7-aa4e-62983c5a37bd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d875178db938e92aa60e3396cee2242d6a54e3f7
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810219"
---
# <a name="sp_help_spatial_geometry_histogram-transact-sql"></a>sp_help_spatial_geometry_histogram (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  空間インデックスの境界ボックスおよびグリッドパラメーターのキーイングを容易にします。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_spatial_geometry_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @xmin = ] 'minx' ]   
     [ , [ @ymin = ] 'miny' ]   
     [ ,.[ @xmax = ] 'maxx' ]  
     [ , [ @ymax = ] 'maxy' ]  
     [ , [ @sample = ] 'sample' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tabname = ] 'tabname'` 空間インデックスが指定されているテーブルの修飾名または修飾され名を指定します。  
  
 引用符は、修飾されたテーブルが指定されている場合にのみ必要です。 データベース名を含む完全修飾名を指定する場合は、データベース名を現在のデータベースの名前にする必要があります。 *tabname* は **sysname**,、既定値はありません。  
  
`[ @colname = ] 'colname'` 指定された空間列の名前を指定します。 *colname* は **sysname**であり、既定値はありません。  
  
`[ @resolution = ] 'resolution'` 境界ボックスの解像度です。 有効な値は 10 ～ 5000 です。 *解決策* は **tinyint**,、既定値はありません。  
  
`[ @xmin = ] 'xmin'` "X の最小値" 境界ボックスプロパティです。 *xmin* は **float**,、既定値はありません。  
  
`[ @ymin = ] 'ymin'` "Y の最小値" 境界ボックスプロパティです。 *ymin* は **float**,、既定値はありません。  
  
`[ @xmax = ] 'xmax'` は、"X の最大値" 境界ボックスプロパティです。 *xmax* は **float**,、既定値はありません。  
  
`[ @ymax = ] 'ymax'` "Y の最大値" 境界ボックスプロパティです。 *ymax* は **float**,、既定値はありません。  
  
`[ @sample = ] 'sample'` 使用するテーブルの割合を示します。 有効な値は 0 ~ 100 です。 *sample* は **float**です。 既定値は100です。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 テーブル値が返されます。 次のグリッドでは、テーブルの列の内容について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|各セルの一意の ID を表します。カウントは1から始まります。|  
|**cell**|**geometry**|それぞれのセルを表す四角形です。 セルの形は、空間インデックス作成用に使用されたセルの形と同じです。|  
|**row_count**|**bigint**|セルをタッチまたは格納している空間オブジェクトの数を示します。|  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、 **public** ロールのメンバーである必要があります。 サーバーとオブジェクトに対する読み取りアクセス権限が必要です。  
  
## <a name="remarks"></a>注釈  
 SSMS 空間タブでは、結果がグラフィカルに表示されます。 空間ウィンドウに対して結果にクエリを実行すると、結果項目の概数を取得できます。 テーブル内のオブジェクトは複数のセルに対応している場合があるため、セルの合計が実際のオブジェクトの数よりも大きくなる可能性があります。  
  
 境界ボックスの外部にあるオブジェクトまたは境界ボックスの境界に接しているオブジェクトの数を格納する追加の行が結果セットに追加される場合があります。 この行の **cellid** は0で、この行の **セル** には、境界ボックスを表す **LineString** が含まれています。 この行は、境界ボックス外の領域全体を表します。  
  
## <a name="examples"></a>例  
 次の例では、サンプルテーブルを作成し、テーブルに対して **sp_help_spatial_geometry_histogram** を呼び出します。  
  
 `USE AdventureWorksDW2012`  
  
 `GO`  
  
 `-- Set database compatibility for circular arc segments`  
  
 `ALTER DATABASE AdventureWorksDW2012`  
  
 `SET COMPATIBILITY_LEVEL = 110;`  
  
 `GO`  
  
 `-- Create table to execute sp_help_spatial_geometry_histogram on`  
  
 `CREATE TABLE TownSites`  
  
 `(`  
  
 `Location geometry NULL,`  
  
 `SiteName nvarchar(50) NULL`  
  
 `)`  
  
 `GO`  
  
 `-- Insert site data into table`  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('POINT(0 0)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Booth Map';`  
  
 `SET @g = geometry::Parse('POLYGON((1 1, 1 2, 2 2, 2 1, 1 1))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Town Hall';`  
  
 `SET @g = geometry::Parse('CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-1 0, 0 -1, 1 0),(1 0, 1 2, -1 0)))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Park';`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(1 5, 2 2, 5 1)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Road';`  
  
 `-- Call proc to see data within bounding box`  
  
 `EXEC sp_help_spatial_geometry_histogram @tabname = TownSites, @colname = Location, @resolution = 64, @xmin = -2, @ymin = -2, @xmax = 3, @ymax = 3, @sample = 100;`  
  
 `GO`  
  
 `DROP TABLE TownSites;`  
  
 `GO`  
  
## <a name="see-also"></a>参照  
 [空間インデックスストアドプロシージャ &#40;Transact-sql&#41;](./spatial-index-stored-procedures-arguments-and-properties.md)  
  
