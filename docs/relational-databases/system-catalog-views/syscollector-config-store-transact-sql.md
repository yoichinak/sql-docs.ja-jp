---
description: syscollector_config_store (Transact-sql)
title: syscollector_config_store (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_config_store_TSQL
- syscollector_config_store
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_config_store view
ms.assetid: f15f6b05-6808-4b76-b6a8-48dec844cf63
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4ceeb3ad0d977282c88314a7305099f7c0db0496
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537685"
---
# <a name="syscollector_config_store-transact-sql"></a>syscollector_config_store (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクションセットのインスタンスではなく、データコレクター全体に適用されるプロパティを返します。 このビューの各行は、管理データ ウェアハウスの名前や、管理データ ウェアハウスが置かれているインスタンスの名前など、データ コレクターの特定のプロパティを表します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|parameter_name|**nvarchar(128)**|プロパティの名前。 NULL 値は許可されません。|  
|parameter_value|**sql_variant**|プロパティの実際の値。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 ビューの SELECT 権限、または dc_operator、dc_proxy、dc_admin のいずれかの固定データベース ロールのメンバーシップが必要です。  
  
## <a name="remarks"></a>解説  
 使用できるプロパティの一覧は固定されており、それらの値は適切なストアドプロシージャを使用してのみ変更できます。 次の表で、このビューを介して公開されるプロパティについて説明します。  
  
|プロパティ名|説明|  
|-------------------|-----------------|  
|CacheDirectory|コレクター型のパッケージが一時的な情報を格納するファイル システム内のディレクトリの名前です。<br /><br /> NULL = 既定の一時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリが使用されます。|  
|キャッシュウィンドウ|データのアップロードに失敗した場合のキャッシュディレクトリのデータ保持ポリシーを示します。<br /><br /> -1 = アップロード エラーが発生した場合は常にデータを保持します。<br /><br /> 0 = アップロード エラーが発生した場合にデータを保持しません。<br /><br /> *n* = 以前のアップロードエラーの *データを保持* します。 *n* >= 1 です。<br /><br /> この値を変更するには、sp_syscollector_set_cache_window ストアド プロシージャを使用します。|  
|CollectorEnabled|データ コレクターの状態を示します。<br /><br /> 0 = 無効<br /><br /> 1 = 有効<br /><br /> この値を変更するには、sp_syscollector_enable_collector ストアド プロシージャまたは sp_syscollector_disable_collector ストアド プロシージャを使用します。|  
|MDWDatabase|管理データウェアハウスの名前。 この値を変更するには、sp_syscollector_set_warehouse_database_name ストアド プロシージャを使用します。|  
|なっ|管理データ ウェアハウスが存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前です。 この値を変更するには、sp_syscollector_set_warehouse_instance_name ストアド プロシージャを使用します。|  
  
## <a name="examples"></a>例  
 次の例では、syscollector_config_store ビューのクエリを実行します。  
  
```sql  
SELECT parameter_name, parameter_value  
FROM msdb.dbo.syscollector_config_store;  
```  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [sp_syscollector_set_warehouse_database_name &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)   
 [sp_syscollector_set_warehouse_instance_name &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
