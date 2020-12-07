---
description: TABLE_CONSTRAINTS (Transact-sql)
title: TABLE_CONSTRAINTS (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- TABLE_CONSTRAINTS
- TABLE_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.TABLE_CONSTRAINTS view
- TABLE_CONSTRAINTS view
ms.assetid: 687f3284-2849-4853-8a5c-fc936deceae0
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5d1b2b7fde378416f83bf749f4be5020ab4aedf1
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753926"
---
# <a name="table_constraints-transact-sql"></a>TABLE_CONSTRAINTS (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベース内のテーブル制約ごとに1行のデータを返します。 この情報スキーマビューでは、現在のユーザーがアクセス許可を持っているオブジェクトに関する情報が返されます。  
  
 これらのビューから情報を取得するには、INFORMATION_SCHEMA の完全修飾名を指定し **ます。**_view_name_。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|制約修飾子。|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|制約を含むスキーマの名前。<br /><br /> <strong> \* \* 重要 \* : \* </strong>オブジェクトのスキーマを検索する信頼できる方法は、sys. objects カタログビューに対してクエリを実行することだけです。|  
|**CONSTRAINT_NAME**|**sysname**|制約名。|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|テーブル修飾子。|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|テーブルを含むスキーマの名前。<br /><br /> <strong> \* \* 重要 \* : \* </strong>オブジェクトのスキーマを検索する信頼できる方法は、sys. objects カタログビューに対してクエリを実行することだけです。|  
|**TABLE_NAME**|**sysname**|テーブル名。|  
|**CONSTRAINT_TYPE**|**varchar (** 11 **)**|制約の種類:<br /><br /> チェック<br /><br /> UNIQUE<br /><br /> PRIMARY KEY<br /><br /> FOREIGN KEY|  
|**IS_DEFERRABLE**|**varchar (** 2 **)**|制約チェックを遅延できるかどうかを指定します。 常に NO が返されます。|  
|**INITIALLY_DEFERRED**|**varchar (** 2 **)**|制約チェックが最初に延期されているかどうかを示します。 常に NO が返されます。|  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)   
 [情報スキーマビュー &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.key_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.check_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
