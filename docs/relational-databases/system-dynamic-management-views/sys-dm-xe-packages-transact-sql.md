---
description: sys.dm_xe_packages (Transact-SQL)
title: sys.dm_xe_packages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_packages_TSQL
- sys.dm_xe_packages_TSQL
- dm_xe_packages
- sys.dm_xe_packages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_packages dynamic management view
- extended events [SQL Server], views
ms.assetid: 2e5ecbe9-3ea8-45e6-a161-e31671a03e1d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: f4d23f493b669744f0c3bb53b6148056131ebe17
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98093932"
---
# <a name="sysdm_xe_packages-transact-sql"></a>sys.dm_xe_packages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  拡張イベントエンジンに登録されているすべてのパッケージを一覧表示します。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|name|**nvarchar (256)**|パッケージの名前。 説明は、パッケージ自体から公開されます。 NULL 値は許可されません。|  
|guid|**uniqueidentifier**|パッケージを識別する GUID。 NULL 値は許可されません。|  
|description|**nvarchar (3072)**|パッケージの説明。 descriptionis パッケージ作成者によって設定され、null 値は許容されません。|  
|capabilities|**int**|このパッケージの機能を説明するビットマップ。 NULL 値が許可されます。|  
|capabilities_desc|**nvarchar (256)**|このパッケージで可能なすべての機能の一覧です。 NULL 値が許可されます。|  
|module_guid|**nvarchar(60)**|このパッケージを公開するモジュールの GUID。 NULL 値は許可されません。|  
|module_address|**varbinary (8)**|パッケージが格納されているモジュールが読み込まれるベースアドレス。 1 つのモジュールで複数のパッケージが公開される場合があります。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="remarks"></a>解説  
 拡張イベント エンジンに登録されているパッケージでは、イベント、イベントの発生時に実行できるアクション、およびイベント データの同期処理および非同期処理の対象が公開されます。  
  
 これらのパッケージは、プロセスのアドレス空間に動的に読み込むことができます。 パッケージが読み込まれるときに、拡張イベントエンジンによって公開されるすべてのオブジェクトが登録されます。  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
| 差出人 | 終了 | Relationship |
| ---- | -- | ------------ |  
|sys.dm_xe_packages.module_address|sys.dm_os_loaded_modules.base_address|多対一|  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

