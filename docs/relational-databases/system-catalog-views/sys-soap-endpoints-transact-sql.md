---
description: soap_endpoints (Transact-sql)
title: soap_endpoints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- soap_endpoints_TSQL
- sys.soap_endpoints
- soap_endpoints
- sys.soap_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.soap_endpoints catalog view
ms.assetid: f50dcbfc-02ed-4a19-9c07-c78a5a1b3224
author: markingmyname
ms.author: maghan
ms.openlocfilehash: daba746b3bbaf198160855e6caa85fb3d7b4fd1d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539503"
---
# <a name="syssoap_endpoints-transact-sql"></a>soap_endpoints (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 SOAP 型ペイロードを保持する、サーバー内のエンドポイントごとに1行の値を格納します。 このビューのすべての行には、HTTP 構成メタデータを保持する、 **http_endpoints**カタログビューに同じ**endpoint_id**を持つ対応する行があります。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**< 継承された列>**||このビューが継承する列の一覧については、「 [sys. エンドポイント &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)」を参照してください。|  
|**is_sql_language_enabled**|**bit**|1 = バッチ = ENABLED オプションが指定されました。これは、エンドポイントでアドホック SQL バッチが許可されることを意味します。|  
|**wsdl_generator_procedure**|**nvarchar (776)**|このメソッドを実装するストアド プロシージャの、3 つの要素で構成される名前。<br /><br /> メソッドの名前は、3 つの要素で構成する必要があります。 1つ、2つ、または4部構成の名前は使用できません。|  
|**default_database**|**sysname**|DATABASE = オプションで指定された既定のデータベースの名前。<br /><br /> NULL = DEFAULT が指定されています。|  
|**default_namespace**|**nvarchar (384)**|NAMESPACE = オプションで指定された既定の名前空間 `https://tempuri.org` 。代わりに default が指定された場合は。|  
|**default_result_schema**|**tinyint**|SCHEMA = オプションの既定値。<br /><br /> 0 = NONE<br /><br /> 1 = 標準|  
|**default_result_schema_desc**|**nvarchar(60)**|SCHEMA = オプションの既定値の説明。<br /><br /> NONE<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 = CHARACTER_SET = SQL オプションが指定されました。<br /><br /> 1 = CHARACTER_SET = XML オプションが指定されました。|  
|**is_session_enabled**|**bit**|0 は、SESSION = DISABLE オプションが指定されていることを示します。<br /><br /> 1 = SESSION = ENABLED オプションが指定されました。|  
|**session_timeout**|**int**|SESSION_TIMEOUT = オプションで指定された値。|  
|**login_type**|**nvarchar(60)**|このエンドポイントで許可されている認証の種類。<br /><br /> WINDOWS<br /><br /> MIXED|  
|**header_limit**|**int**|SOAP ヘッダーの最大許容サイズ。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
