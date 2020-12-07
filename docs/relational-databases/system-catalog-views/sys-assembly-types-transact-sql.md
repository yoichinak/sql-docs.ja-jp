---
description: assembly_types (Transact-sql)
title: assembly_types (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 06eb2eb4fe6b0983b798ea38fa98057be73af77a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545089"
---
# <a name="sysassembly_types-transact-sql"></a>assembly_types (Transact-sql)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  CLR アセンブリによって定義されるユーザー定義型ごとに 1 行のデータを保持します。 次の**assembly_types**は、 **rule_object_id**後に、継承された列の一覧に表示されます (例については、「 [transact-sql&#41;&#40;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)」を参照してください)。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|この型の作成元であるアセンブリの ID です。|  
|**assembly_class**|**sysname**|この型を定義しているアセンブリ内のクラスの名前です。|  
|**is_binary_ordered**|**bit**|この型のバイトの並べ替えは、型の比較演算子を使用した並べ替えと同じです。|  
|**is_fixed_length**|**bit**|型の長さは、常に max_length と同じです。|  
|**prog_id**|**nvarchar(40)**|COM に公開される型の ProgID。|  
|**assembly_qualified_name**|**nvarchar (4000)**|アセンブリ修飾型名。 この名前は、タイプ GetType () に渡すのに適した形式になっています。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;スカラー型のカタログビュー ](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
