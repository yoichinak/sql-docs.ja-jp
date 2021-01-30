---
description: sp_help_spatial_geography_index_xml (Transact-sql)
title: sp_help_spatial_geography_index_xml (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_help_spatial_geography_index_xml_TSQL
- sp_help_spatial_geography_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index_xml procedure
ms.assetid: 821d4127-3ce5-4474-8561-043404a20d81
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81bad34a1eb0d45eafb84bacf1cc65871e73e2b9
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99158431"
---
# <a name="sp_help_spatial_geography_index_xml-transact-sql"></a>sp_help_spatial_geography_index_xml (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Geography** 空間インデックスに関する指定された一連のプロパティの名前と値を返します。 プロパティのコアセットとインデックスのすべてのプロパティのどちらを返すかを選択できます。  
  
 結果は、選択したプロパティの名前と値を表示する XML フラグメントで返されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_spatial_geography_index_xml [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>引数  
 「 [空間インデックスストアドプロシージャの引数とプロパティ」を](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)参照してください。  
  
## <a name="properties"></a>Properties  
 「 [空間インデックスストアドプロシージャの引数とプロパティ」を](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 プロシージャにアクセスするには、ユーザーに PUBLIC ロールが割り当てられている必要があります。 サーバーとオブジェクトに対する読み取りアクセス権限が必要です。  
  
## <a name="remarks"></a>コメント  
 NULL 値を含むプロパティは、返されるセットに含まれません。  
  
## <a name="example"></a>例  
 次の例では、を使用し `sp_help_spatial_geography_index_xml` て、 **\@ qs** の指定されたクエリサンプルのテーブル **geography_col** で定義されている空間インデックス **SIndx_SpatialTable_geography_col2** を調査します。 この例では、選択したプロパティの名前と値を表示する XML フラグメント内の指定されたインデックスのコアプロパティを返します。  
  
 その後、 [XQuery](../../xquery/xquery-basics.md) が結果セットで実行され、特定のプロパティが返されます。  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
declare @x xml;  
exec sp_help_spatial_geography_index_xml 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs, @x output;  
select @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 [Sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)と同様に、このストアドプロシージャを使用すると、**地理** 空間インデックスのプロパティにプログラムで簡単にアクセスして、XML 形式で結果セットを報告できます。  
  
 **Geography** の境界ボックスは、地球全体です。  
  
## <a name="requirements"></a>必要条件  
  
## <a name="see-also"></a>参照  
 [空間インデックスストアドプロシージャ](./spatial-index-stored-procedures-arguments-and-properties.md)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空間データ &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [XQuery の基礎](../../xquery/xquery-basics.md)   
 [XQuery 言語リファレンス](../../xquery/xquery-language-reference-sql-server.md)  
  
