---
description: DOMAIN_CONSTRAINTS (Transact-sql)
title: DOMAIN_CONSTRAINTS (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAIN_CONSTRAINTS
- DOMAIN_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.DOMAIN_CONSTRAINTS view
- DOMAIN_CONSTRAINTS view
ms.assetid: 436c4480-f1e3-403f-b2bd-de04539afe3c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 20f675d11a58af2f5a1a433b8fdba41d07d4b01b
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753576"
---
# <a name="domain_constraints-transact-sql"></a>DOMAIN_CONSTRAINTS (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベース内で、ルールがバインドされていて現在のユーザーがアクセスできる、別名データ型ごとに1行のデータを返します。  
  
 これらのビューから情報を取得するには、INFORMATION_SCHEMA の完全修飾名を指定し **ます。**_view_name_。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|ルールが存在するデータベース。|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|制約を含むスキーマの名前。<br /><br /> 重要オブジェクトのスキーマを決定するために INFORMATION_SCHEMA ビューを使用しないでください。 <strong> \* \* \* \* </strong> INFORMATION_SCHEMA ビューは、オブジェクトのメタデータのサブセットのみを表します。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**CONSTRAINT_NAME**|**sysname**|[規則名]。|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|別名データ型が存在するデータベース。|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|別名データ型を含むスキーマの名前<br /><br /> 重要データ型のスキーマを決定するために INFORMATION_SCHEMA ビューを使用しないでください。 <strong> \* \* \* \* </strong> 型のスキーマを検索する唯一の信頼性のある方法は、TYPEPROPERTY 関数を使用することです。|  
|**DOMAIN_NAME**|**sysname**|別名データ型。|  
|**IS_DEFERRABLE**|**varchar (** 2 **)**|制約チェックを遅延できるかどうかを指定します。 常に NO が返されます。|  
|**INITIALLY_DEFERRED**|**varchar (** 2 **)**|制約チェックが最初に延期されているかどうかを示します。 常に NO が返されます。|  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)   
 [情報スキーマビュー &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
