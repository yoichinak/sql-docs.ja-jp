---
description: Azure Synapse Analytics ストアドプロシージャ
title: Azure Synapse Analytics ストアドプロシージャ
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02e04dfe-d565-4e45-b427-b8e89c958ba3
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 080808c2f32990070ab630042a00e2173f0440a2
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92059540"
---
# <a name="azure-synapse-analytics-stored-procedures"></a>Azure Synapse Analytics ストアドプロシージャ
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] には、データベースロールに関連する操作を実行するために使用できる組み込みの手順が用意されています。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] には、次のシステムプロシージャが含まれています。  
  
<a name="AggregateFunctions"></a>[sp_datatype_info_90 &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-datatype-info-90-sql-data-warehouse.md)  
  
 [sp_pdw_add_network_credentials &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
 [sp_pdw_log_user_data_masking &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
 [sp_pdw_remove_network_credentials &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
 [sp_special_columns_100 &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-special-columns-100-sql-data-warehouse.md)  
  
> [!NOTE]  
>  いくつかの追加のシステムストアドプロシージャは、のインスタンス内 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはクライアント api を使用してのみ使用され、一般的な顧客使用を目的としていません。 これらの手順については、 [「システムストアドプロシージャ (transact-sql)](./system-stored-procedures-transact-sql.md)」をご覧ください。 これらの手順は変更される可能性があり、互換性は保証されません。 この一覧に記載されているすべてのプロシージャは、では使用できません [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。  
  
## <a name="see-also"></a>関連項目  
 [システムストアド関数 &#40;Transact-sql&#41;](~/relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
