---
description: sys.dm_db_objects_impacted_on_version_change (Azure SQL データベース)
title: sys.dm_db_objects_impacted_on_version_change
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_objects_impacted_on_version_change_TSQL
- dm_db_objects_impacted_on_version_change
- dm_db_objects_impacted_on_version_change_TSQL
- sys.dm_db_objects_impacted_on_version_change
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_objects_impacted_on_version_change
- sys.dm_db_objects_impacted_on_version_change
ms.assetid: b94af834-c4f6-4a27-80a6-e8e71fa8793a
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: c316d1f87b76387ebf382754970a6b9dc1ab609f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89517772"
---
# <a name="sysdm_db_objects_impacted_on_version_change-azure-sql-database"></a>sys.dm_db_objects_impacted_on_version_change (Azure SQL データベース)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  このデータベーススコープシステムビューは、のメジャーリリースアップグレードによって影響を受けるオブジェクトを決定するための早期警告システムを提供するように設計されてい [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] ます。 このビューを使用すると、アップグレードの前または後に、影響を受けるすべてのオブジェクトのリストを取得できます。 このビューは各データベースでクエリし、サーバー全体での完全な情報を取得する必要があります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|class|**int** NULL 以外|影響を受けるオブジェクトのクラス。<br /><br /> **1** = 制約<br /><br /> **7** = インデックスとヒープ|  
|class_desc|**nvarchar (60)** NULL 以外|クラスの説明:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **INDEX**|  
|major_id|**int** NULL 以外|制約のオブジェクト ID、あるいはインデックスまたはヒープを含んでいるテーブルのオブジェクト ID。|  
|minor_id|**int** 空白|制約の場合は **NULL**<br /><br /> インデックスおよびヒープの場合は Index_id|  
|dependency|**nvarchar (60)** NULL 以外|制約またはインデックスが影響を受ける原因となっている依存関係の説明。 アップグレード中に生成される警告にも同じ値が使用されます。<br /><br /> 次に例を示します。<br /><br /> **space** (組み込み用)<br /><br /> **geometry** (システム UDT 用)<br /><br /> **geography::Parse** (システム UDT メソッド用)|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW DATABASE STATE 権限が必要です。  
  
## <a name="example"></a>例  
 次の例は、次回の主要なサーバー バージョンへのアップグレードによって影響を受けるオブジェクトを検索するための、**sys.dm_db_objects_impacted_on_version_change** に対するクエリを示します。  
  
```  
SELECT * FROM sys.dm_db_objects_disabled_on_version_change;  
GO  
```  
  
```  
class  class_desc        major_id    minor_id    dependency                       
------ ----------------- ----------- ----------- ----------   
1      OBJECT_OR_COLUMN  181575685   NULL        geometry                        
7      INDEX             37575172    1           geometry                        
7      INDEX             2121058592  1           geometry                        
1      OBJECT_OR_COLUMN  101575400   NULL        geometry     
```  
  
## <a name="remarks"></a>解説  
  
### <a name="how-to-update-impacted-objects"></a>影響を受けるオブジェクトを更新する方法  
 次の手順は、次の 6 月のサービス リリースのアップグレード後に行う必要のある修正措置を説明しています。  
  
|Order|影響を受けるオブジェクト|修正措置|  
|-----------|---------------------|-----------------------|  
|1|**インデックス**|次の例のように、dm_db_objects_impacted_on_version_change によって識別されるインデックスを再構築 **し** ます。  `ALTER INDEX ALL ON <table> REBUILD`<br />or<br />`ALTER TABLE <table> REBUILD`|  
|2|**Object**|**sys.dm_db_objects_impacted_on_version_change** で識別されるすべての制約は、基になるテーブルの geometry 型および geography 型のデータが再計算された後に再検証する必要があります。 制約に対しては、ALTER TABLE を使用して再検証します。 <br />次に例を示します。 <br />`ALTER TABLE <tab> WITH CHECK CHECK CONSTRAINT <constraint name>`<br />or<br />`ALTER TABLE <tab> WITH CHECK CONSTRAINT ALL`|  
  
  
