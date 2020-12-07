---
description: syscollector_collector_types (Transact-sql)
title: syscollector_collector_types (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collector_types
- syscollector_collector_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collector_types view
ms.assetid: d5cd30bb-89fd-4814-a7e8-9074f043f90f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 694f14e95c0bec4edaf94c7a2c8a3885ad841c24
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537287"
---
# <a name="syscollector_collector_types-transact-sql"></a>syscollector_collector_types (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクション アイテムのコレクターの種類に関する情報を提供します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifer**|コレクション型の GUID。 NULL 値は許可されません。|  
|**name**|**sysname**|コレクション型の名前。 NULL 値は許可されません。|  
|**parameter_schema**|**xml**|指定されたコレクターの種類の構成を記述する XML スキーマ。 この XML スキーマは、特定のコレクションアイテムインスタンスに関連付けられた実際の XML 構成を検証するために使用されます。 NULL 値が許可されます。|  
|**parameter_formatter**|**xml**|コレクションセットのプロパティページで使用する XML を変換するために使用するテンプレートを指定します。 NULL 値が許可されます。|  
|**collection_package_id**|**uniqueidentifer**|コレクションパッケージの GUID。 NULL 値は許可されません。|  
|**collection_package_path**|**nvarchar (4000)**|コレクションパッケージへのパスを提供します。 NULL 値が許可されます。|  
|**collection_package_name**|**sysname**|コレクションパッケージの名前です。 NULL 値は許可されません。|  
|**upload_package_id**|**uniqueidentifer**|アップロード パッケージの GUID。 NULL 値は許可されません。|  
|**upload_package_path**|**nvarchar (4000)**|アップロード パッケージのパス。 NULL 値が許可されます。|  
|**upload_package_name**|**sysname**|アップロードパッケージの名前です。 NULL 値は許可されません。|  
|**is_system**|**bit**|コレクター型がデータコレクターに付属しているかどうか、または後で **dc_admin**によって追加されたかどうかを示すには、(1) または off (0) をオンにします。 たとえば、社内またはサード パーティによって開発されたカスタム型が考えられます。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 **Dc_operator**、 **dc_proxy**を選択する必要があります。  
  
## <a name="change-history"></a>変更履歴  
  
|変更内容|  
|---------------------|  
|**Collection_type_uid**列名が**collector_type_uid**に更新されました。|  
|**Parameter_schema**列の説明を、null 値が許容される値であることを示すように修正しました。|  
|**Parameter_formatter**列を追加しました。|  
|**Collection_package_path**列のデータ型を修正し、値が null 許容であることを示す説明を更新しました。|  
|**Upload_package_path**列のデータ型を修正し、値が null 許容であることを示す説明を更新しました。|  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
