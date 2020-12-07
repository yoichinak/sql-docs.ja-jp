---
description: sys.xml_schema_collections (Transact-SQL)
title: sys.xml_schema_collections (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_collections_TSQL
- sys.xml_schema_collections
- xml_schema_collections
- xml_schema_collections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_collections catalog view
ms.assetid: f3f7f3dc-029f-4942-ab3c-75fa9814e40f
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d54502963e0a6464d4a437a46c83db53667bab5a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400738"
---
# <a name="sysxml_schema_collections-transact-sql"></a>sys.xml_schema_collections (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  XML スキーマコレクションごとに1行の値を返します。 XML スキーマ コレクションは、名前付きの XSD 定義セットです。 XML スキーマ コレクション自体はリレーショナル スキーマに含まれ、スキーマ スコープの [!INCLUDE[tsql](../../includes/tsql-md.md)] 名で識別されます。 xml_collection_id、schema_id、および name の組は一意です。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|xml_collection_id|**int**|XML スキーマコレクションの ID。 データベース内で一意です。|  
|schema_id|**int**|XML スキーマ コレクションを含むリレーショナル スキーマの ID。|  
|principal_id|**int**|スキーマの所有者と異なる場合は、個々の所有者の ID。 既定では、スキーマに含まれるオブジェクトはスキーマの所有者によって所有されます。 ただし、ALTER AUTHORIZATION ステートメントを使用して所有権を変更することによって、代替所有者を指定できます。<br /><br /> NULL = 別の個別所有者ではありません。|  
|name|**sysname**|XML スキーマコレクションの名前。|  
|create_date|**datetime**|XML スキーマコレクションが作成された日付。|  
|modify_date|**datetime**|XML スキーマ コレクションが最後に変更された日付。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml スキーマ &#40;XML 型システム&#41; カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
