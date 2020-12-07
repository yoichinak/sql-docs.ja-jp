---
description: ROUTINE_COLUMNS (Transact-sql)
title: ROUTINE_COLUMNS (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- ROUTINE_COLUMNS_TSQL
- ROUTINE_COLUMNS
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINE_COLUMNS view
- INFORMATION_SCHEMA.ROUTINE_COLUMNS view
ms.assetid: 91dbc61b-e4c0-4826-976c-b2fce88b7793
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ec57f41be3971b41d5bebf6c139b9913666e8c20
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753971"
---
# <a name="routine_columns-transact-sql"></a>ROUTINE_COLUMNS (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベース内の、現在のユーザーがアクセスできるテーブル値関数によって返される列ごとに、1 行のデータを返します。  
  
 このビューから情報を取得するには、INFORMATION_SCHEMA の完全修飾名を指定し **ます。**_view_name_。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|テーブル値関数のカタログ名またはデータベース名。|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|テーブル値関数を含むスキーマの名前。<br /><br /> 重要オブジェクトのスキーマを決定するために INFORMATION_SCHEMA ビューを使用しないでください。 <strong> \* \* \* \* </strong> INFORMATION_SCHEMA ビューは、オブジェクトのメタデータのサブセットのみを表します。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|テーブル値関数の名前。|  
|**COLUMN_NAME**|**nvarchar (** 128 **)**|列名。|  
|**ORDINAL_POSITION**|**int**|列の識別番号。|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|列の既定値です。|  
|**IS_NULLABLE**|**varchar (** 3 **)**|この列が NULL 値を許容する場合、は YES を返します。 その他の場合は NO が返されます。|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|システムにより提供されるデータ型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|バイナリ データ、文字データ、またはテキストおよびイメージ データの最大文字列長。<br /><br /> **xml**と大きな値の型のデータの場合は-1。 その他の場合は NULL が返されます。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。|  
|**CHARACTER_OCTET_LENGTH**|**int**|バイナリ データ、文字データ、またはテキストおよびイメージ データの最大バイト長。<br /><br /> **xml**と大きな値の型のデータの場合は-1。 その他の場合は NULL が返されます。|  
|**NUMERIC_PRECISION**|**tinyint**|数値データの概数、正確な数値データ、整数データ、または通貨データの有効桁数。 その他の場合は NULL が返されます。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|数値データの概数、正確な数値データ、整数データ、または通貨データの有効桁数の基数。 その他の場合は NULL が返されます。|  
|**NUMERIC_SCALE**|**tinyint**|数値データの概数、正確な数値データ、整数データ、または通貨データの桁数。 その他の場合は NULL が返されます。|  
|**DATETIME_PRECISION**|**smallint**|**Datetime**および ISO**整数**データ型のサブタイプコード。 その他のデータ型の場合は、NULL を返します。|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|**Master**を返します。 これは、列が文字データまたは **テキスト** データ型の場合に、文字セットが配置されているデータベースを示します。 その他の場合は NULL が返されます。|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|常に NULL が返されます。|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|この列が文字データまたは **テキスト** データ型の場合、文字セットの一意の名前を返します。 その他の場合は NULL が返されます。|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|常に NULL が返されます。|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|常に NULL が返されます。|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|列が文字データまたは **テキスト** データ型の場合、並べ替え順序の一意な名前を返します。 その他の場合は NULL が返されます。|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|列が別名データ型の場合、この列はユーザー定義データ型が作成されたデータベース名になります。 その他の場合は NULL が返されます。|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|列がユーザー定義データ型の場合、この列はユーザー定義データ型を含むスキーマの名前です。 その他の場合は NULL が返されます。<br /><br /> 重要オブジェクトのスキーマを決定するために INFORMATION_SCHEMA ビューを使用しないでください。 <strong> \* \* \* \* </strong> INFORMATION_SCHEMA ビューは、オブジェクトのメタデータのサブセットのみを表します。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**DOMAIN_NAME**|**nvarchar (** 128 **)**|列がユーザー定義データ型の場合、この列はユーザー定義データ型の名前になります。 その他の場合は NULL が返されます。|  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)   
 [情報スキーマビュー &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
