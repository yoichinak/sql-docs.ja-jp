---
description: sys.system_components_surface_area_configuration (Transact-sql)
title: sys.system_components_surface_area_configuration (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.system_components_surface_area_configuration_TSQL
- system_components_surface_area_configuration
- system_components_surface_area_configuration_TSQL
- sys.system_components_surface_area_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_components_surface_area_configuration catalog view
ms.assetid: d9920008-3387-4f9e-8f21-47473f2ba04f
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 07cce3c6c49609843baa1b2cb5c3a463260a3ab4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99195149"
---
# <a name="syssystem_components_surface_area_configuration-transact-sql"></a>sys.system_components_surface_area_configuration (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  セキュリティ構成コンポーネントによって有効または無効にできる実行可能なシステムオブジェクトごとに1行の値を返します。 詳細については、「 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**component_name**|**sysname**|コンポーネント名。 これには、キーワード collation、Latin1_General_CI_AS_KS_WS が設定されます。 Nll は指定できません。|  
|**database_name**|**sysname**|オブジェクトを含むデータベースです。 これには、キーワード collation、Latin1_General_CI_AS_KS_WS が設定されます。 次のいずれかである必要があります。<br /><br /> **master**<br /><br /> **msdb**<br /><br /> **mssqlsystemresource**|  
|**schema_name**|**sysname**|オブジェクトを含むスキーマです。 これには、キーワード collation、Latin1_General_CI_AS_KS_WS が設定されます。 Nll は指定できません。|  
|**object_name**|**sysname**|オブジェクト名。 これには、キーワード collation、Latin1_General_CI_AS_KS_WS が設定されます。 Nll は指定できません。|  
|**state**|**tinyint**|0 = 無効<br /><br /> 1 = 有効|  
|**type**|**char(2)**|オブジェクトの種類です。 以下のいずれかを指定できます。<br /><br /> P = SQL_STORED_PROCEDURE<br /><br /> PC = CLR_STORED_PROCEDURE<br /><br /> FN = SQL_SCALAR_FUNCTION<br /><br /> FS = CLR_SCALAR_FUNCTION<br /><br /> FT = CLR_TABLE_VALUED_FUNCTION<br /><br /> IF = SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> TF = SQL_TABLE_VALUED_FUNCTION<br /><br /> X = EXTENDED_STORED_PROCEDURE|  
|**type_desc**|**nvarchar(60)**|オブジェクトの種類のわかりやすい名前。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
