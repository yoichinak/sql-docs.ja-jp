---
description: DOMAINS (Transact-SQL)
title: DOMAINS (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAINS_TSQL
- DOMAINS
dev_langs:
- TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c7237d75abfcc67dc1045896cd095cea4f78123
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753618"
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベースの現在のユーザーがアクセスできる別名データ型ごとに1行のデータを返します。  
  
 これらのビューから情報を取得するには、INFORMATION_SCHEMA の完全修飾名を指定し **ます。**_view_name_。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|別名データ型が存在するデータベース。|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|別名データ型を含むスキーマの名前。<br /><br /> **&#42;&#42; の重要な &#42;&#42;** データ型のスキーマを決定するために INFORMATION_SCHEMA ビューを使用しないでください。 型のスキーマを検索する唯一の信頼性のある方法は、TYPEPROPERTY 関数を使用することです。|  
|**DOMAIN_NAME**|**sysname**|別名データ型。|  
|**DATA_TYPE**|**sysname**|システムにより提供されるデータ型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|バイナリ データ、文字データ、またはテキストおよびイメージ データの最大文字列長。<br /><br /> **xml**と大きな値の型のデータの場合は-1。 その他の場合は NULL が返されます。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。|  
|**CHARACTER_OCTET_LENGTH**|**int**|バイナリ データ、文字データ、またはテキストおよびイメージ データの最大バイト長。<br /><br /> **xml**と大きな値の型のデータの場合は-1。 その他の場合は NULL が返されます。|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|常に NULL が返されます。|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|常に NULL が返されます。|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|列が文字データまたは **テキスト** データ型の場合、並べ替え順序の一意な名前を返します。 その他の場合は NULL が返されます。|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|**Master**を返します。 列が文字データまたは **テキスト** データ型の場合、文字セットが存在するデータベースを示します。 その他の場合は NULL が返されます。|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|常に NULL が返されます。|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|この列が文字データまたは **テキスト** データ型の場合、文字セットの一意の名前を返します。 その他の場合は NULL が返されます。|  
|**NUMERIC_PRECISION**|**tinyint**|数値データの概数、正確な数値データ、整数データ、または通貨データの有効桁数。 その他の場合は NULL が返されます。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|数値データの概数、正確な数値データ、整数データ、または通貨データの有効桁数の基数。 その他の場合は NULL が返されます。|  
|**NUMERIC_SCALE**|**tinyint**|数値データの概数、正確な数値データ、整数データ、または通貨データの桁数。 その他の場合は NULL が返されます。|  
|**DATETIME_PRECISION**|**smallint**|**Datetime**および ISO **interval**データ型のサブタイプコード。 その他のデータ型の場合、この列は NULL を返します。|  
|**DOMAIN_DEFAULT**|**nvarchar (** 4000 **)**|定義ステートメントの実際のテキスト [!INCLUDE[tsql](../../includes/tsql-md.md)] 。|  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)   
 [情報スキーマビュー &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sys文字セット &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
