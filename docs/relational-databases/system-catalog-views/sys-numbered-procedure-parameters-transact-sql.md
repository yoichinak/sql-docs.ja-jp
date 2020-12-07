---
description: sys.numbered_procedure_parameters (Transact-SQL)
title: numbered_procedure_parameters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- numbered_procedure_parameters_TSQL
- sys.numbered_procedure_parameters_TSQL
- numbered_procedure_parameters
- sys.numbered_procedure_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedure_parameters catalog view
ms.assetid: a441d46d-1f30-41c2-8d94-e9442f59786e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4bb67e0f0063c9ed7469b0a3d9e29a29b8117e22
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539600"
---
# <a name="sysnumbered_procedure_parameters-transact-sql"></a>sys.numbered_procedure_parameters (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  番号付きプロシージャのパラメーターごとに1行の値を格納します。 番号付きストアド プロシージャを作成する場合は、ベース プロシージャの番号が 1 になり、 以降のプロシージャの番号は 2、3 のように続きます。 **numbered_procedure_parameters** には、2番目以降のすべてのプロシージャのパラメーター定義が含まれています。 このビューでは、ベース ストアド プロシージャ (番号 = 1) のパラメーターは示されません。 ベースストアドプロシージャは、番号が付けられていないストアドプロシージャに似ています。 そのため、パラメーターは、 [sys. parameters (transact-sql)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)で表現されます。  
  
> [!IMPORTANT]  
>  番号付きプロシージャは非推奨とされます。 番号付きプロシージャの使用は推奨されません。 このカタログビューを使用するクエリがコンパイルされると、DEPRECATION_ANNOUNCEMENT イベントが発生します。  
  
> [!NOTE]  
>  XML および CLR パラメーターは、番号付きプロシージャではサポートされていません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このパラメーターが属するオブジェクトの ID。|  
|**procedure_number**|**smallint**|オブジェクト内のこのプロシージャの数 (2 以上)。|  
|**name**|**sysname**|パラメーターの名前。 **Procedure_number**内で一意です。|  
|**parameter_id**|**int**|パラメーターの ID。 **Procedure_number**内で一意です。|  
|**system_type_id**|**tinyint**|パラメーターのシステム型の ID|  
|**user_type_id**|**int**|ユーザーが定義した、パラメーターの型の ID。|  
|**max_length**|**smallint**|パラメーターの最大長 (バイト単位)。<br /><br /> -1 = 列のデータ型は varchar (max),、nvarchar (max),、または varbinary (max) です。|  
|**有効桁数 (precision)**|**tinyint**|数値ベースの場合のパラメーターの有効桁数。それ以外の場合は0です。|  
|**scale**|**tinyint**|数値ベースの場合はパラメーターの小数点以下桁数。それ以外の場合は0です。|  
|**is_output**|**bit**|1 = パラメーターは出力または戻り値です。それ以外の場合は 0 です。|  
|**is_cursor_ref**|**bit**|1 = パラメーターはカーソル参照パラメーターです。|  
  
> [!NOTE]  
>  XML および CLR パラメーターは、番号付きプロシージャではサポートされていません。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
