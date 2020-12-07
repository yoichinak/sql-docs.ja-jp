---
description: sys. parameters (Transact-sql)
title: sys. parameters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.parameters_TSQL
- sys.parameters
- parameters
- parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameters catalog view
- table-valued parameters,sys.parameters
ms.assetid: 24e2764b-c8e5-4322-97a4-7407d8b8a92b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 863f360d5d5aaba7eae957d7406f5e3ec465d64f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548718"
---
# <a name="sysparameters-transact-sql"></a>sys. parameters (Transact-sql)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  パラメーターを受け入れるオブジェクトのパラメーターごとに 1 行のデータを保持します。 オブジェクトがスカラー関数の場合、戻り値を説明する単一行も含まれます。 この行の **parameter_id** 値は0です。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このパラメーターが属するオブジェクトの ID。|  
|**name**|**sysname**|パラメーターの名前。 は、オブジェクト内で一意です。<br /><br /> オブジェクトがスカラー関数の場合、パラメーター名は、戻り値を表す行の空の文字列になります。|  
|**parameter_id**|**int**|パラメーターの ID。 は、オブジェクト内で一意です。<br /><br /> オブジェクトがスカラー関数の場合、 **parameter_id** = 0 は戻り値を表します。|  
|**system_type_id**|**tinyint**|パラメーターのシステム型の ID。|  
|**user_type_id**|**int**|ユーザーによって定義されたパラメーターの型の ID。<br /><br /> 型の名前を返すには、この列の [型](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) のカタログビューに結合します。|  
|**max_length**|**smallint**|パラメーターの最大長 (バイト単位)。<br /><br /> 列のデータ型が **varchar (max)**、 **nvarchar (max)**、 **varbinary (max)**、または **xml**の場合、値は-1 になります。|  
|**有効桁数 (precision)**|**tinyint**|数値ベースの場合のパラメーターの有効桁数。それ以外の場合は0です。|  
|**scale**|**tinyint**|数値ベースの場合はパラメーターの小数点以下桁数。それ以外の場合は0です。|  
|**is_output**|**bit**|1 = パラメーターは OUTPUT または RETURN です。それ以外の場合は 0 です。|  
|**is_cursor_ref**|**bit**|1 = パラメーターはカーソル参照パラメーターです。|  
|**has_default_value**|**bit**|1 = パラメーターには既定値があります。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、このカタログ ビュー内の CLR オブジェクトの既定値のみが保持されます。したがって、[!INCLUDE[tsql](../../includes/tsql-md.md)] オブジェクトに対してこの列の値は 0 になります。 オブジェクトのパラメーターの既定値を表示するに [!INCLUDE[tsql](../../includes/tsql-md.md)] は、 [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)カタログビューの**定義**列に対してクエリを実行するか、 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)システム関数を使用します。|  
|**is_xml_document**|**bit**|1 = コンテンツは完全な XML ドキュメントです。<br /><br /> 0 = コンテンツがドキュメントフラグメントであるか、列のデータ型が **xml**ではありません。|  
|**default_value**|**sql_variant**|**Has_default_value**が1の場合、この列の値はパラメーターの既定値になります。それ以外の場合は NULL。|  
|**xml_collection_id**|**int**|パラメーターのデータ型が **xml** で xml が型指定されている場合は0以外の値。 この値は、パラメーターの検証 XML スキーマ名前空間を含むコレクションの ID です。<br /><br /> 0 = XML スキーマコレクションがありません。|  
|**is_readonly**|**bit**|1 = パラメーターは READONLY です。それ以外の場合は0です。|  
|**is_nullable**|**bit**|1 = パラメーターは null 値を許容します。 (既定値)。<br /><br /> 0 = ネイティブコンパイルストアドプロシージャをより効率的に実行するために、パラメーターは null 値を許容しません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システムカタログに対するクエリについてよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [all_parameters &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)   
 [sys.system_parameters &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
