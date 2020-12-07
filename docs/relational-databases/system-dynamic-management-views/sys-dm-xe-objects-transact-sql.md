---
description: sys.dm_xe_objects (Transact-SQL)
title: dm_xe_objects (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_objects
- sys.dm_xe_objects
- sys.dm_xe_objects_TSQL
- dm_xe_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_objects dynamic management view
- extended events [SQL Server], views
ms.assetid: 5d944b99-b097-491b-8cbd-b0e42b459ec0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a0df750dd3f582e712c41a01ce1406586b2cecf6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536898"
---
# <a name="sysdm_xe_objects-transact-sql"></a>sys.dm_xe_objects (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  イベント パッケージによって公開されるオブジェクトごとに 1 行のデータを返します。 オブジェクトには、次のいずれかを指定できます。  
  
-   イベント。 イベントは、実行パス内の関心のあるポイントを示します。 すべてのイベントには、関心のあるポイントに関する情報が含まれています。  
  
-   アクション。 アクションは、イベントが発生したときに同期的に実行されます。 アクションは、実行時データをイベントに追加できます。  
  
-   ターゲット. ターゲットは、イベントを開始したスレッド上で同期的にまたはシステムによって提供されたスレッド上で非同期的に、イベントを使用します。  
  
-   述部. 述語ソースは、比較演算で使用する値をイベント ソースから取得します。 述語の比較では、特定のデータ型が比較され、ブール値が返されます。  
  
-   種類:  型は、バイトコレクションの長さと特性をカプセル化します。これは、データを解釈するために必要です。  

 |列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|オブジェクトの名前。 名前は、特定の種類のオブジェクトのパッケージ内で一意です。 NULL 値は許可されません。|  
|object_type|**nvarchar(60)**|オブジェクトの型。 object_type は次のいずれかです。<br /><br /> event<br /><br /> action<br /><br /> ターゲット (target)<br /><br /> pred_source<br /><br /> pred_compare<br /><br /> 型<br /><br /> NULL 値は許可されません。|  
|package_guid|**uniqueidentifier**|このアクションを公開するパッケージの GUID。 sys.dm_xe_packages.package_id との間に多対一のリレーションシップがあります。 NULL 値は許可されません。|  
|description|**nvarchar (256)**|アクションの説明。 説明はパッケージの作成者によって設定されます。 NULL 値は許可されません。|  
|capabilities|**int**|オブジェクトの機能を説明するビットマップ。 NULL 値が許可されます。|  
|capabilities_desc|**nvarchar (256)**|オブジェクトのすべての機能を一覧表示します。 NULL 値が許可されます。<br /><br /> **すべてのオブジェクトの種類に適用される機能**<br /><br /> -<br />                                **プライベート**。 内部的に使用できる唯一のオブジェクトであり、CREATE/ALTER EVENT SESSION DDL ではアクセスできません。 監査イベントとターゲットは、内部的に使用される少数のオブジェクトに加えて、このカテゴリに分類されます。<br /><br /> ===============<br /><br /> **イベントの機能**<br /><br /> -<br />                                **No_block**。 イベントは、どのような理由でもブロックできない重要なコード パス内にあります。 この機能を持つイベントは、NO_EVENT_LOSS を指定するイベントセッションに追加することはできません。<br /><br /> ===============<br /><br /> **すべてのオブジェクトの種類に適用される機能**<br /><br /> -<br />                                **Process_whole_buffers**。 ターゲットは、イベントごとではなく、イベントのバッファーをまとめて使用します。<br /><br /> -<br />                        **シングルトン**。 プロセスにはターゲットのインスタンスが 1 つだけ存在できます。 複数のイベント セッションで同じシングルトン ターゲットを参照できますが、インスタンスは 1 つだけであり、そのインスタンスが一意の各イベントを 1 回だけ認識します。 これは、すべてが同じイベントを収集する複数のセッションにターゲットが追加される場合に重要です。<br /><br /> -<br />                                **同期**。 ターゲットは、呼び出し元のコード行に制御が返される前に、イベントを生成しているスレッドで実行されます。|  
|type_name|**nvarchar(60)**|pred_source オブジェクトおよび pred_compare オブジェクトの名前。 NULL 値が許可されます。|  
|type_package_guid|**uniqueidentifier**|このオブジェクトの対象となる型を公開するパッケージの GUID。 NULL 値が許可されます。|  
|type_size|**int**|データ型のサイズ (バイト単位)。 これは、有効なオブジェクトの種類に対してのみ使用されます。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|From|終了|リレーションシップ|  
|----------|--------|------------------|  
|sys.dm_xe_objects.package_guid|sys.dm_xe_packages.guid|多対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

