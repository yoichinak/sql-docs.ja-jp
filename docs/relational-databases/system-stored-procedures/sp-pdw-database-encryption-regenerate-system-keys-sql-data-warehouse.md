---
title: sp_pdw_database_encryption_regenerate_system_keys (Azure Synapse Analytics) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: bb13e323-a984-4462-8b6d-6019c38ddd9d
author: ronortloff
ms.author: rortloff
ms.reviewer: ''
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f432d19a558b82abd52bef2839c0887dff70f7ba
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92254759"
---
# <a name="sp_pdw_database_encryption_regenerate_system_keys-azure-synapse-analytics"></a>sp_pdw_database_encryption_regenerate_system_keys (Azure Synapse Analytics)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  アプライアンスで TDE が有効になっているときに暗号化される内部データベースの証明書とデータベース暗号化キーをローテーションするには、 **sp_pdw_database_encryption_regenerate_system_keys** を使用します。 ここには、`tempdb` が含まれています。 これは、TDE が有効になっている場合にのみ成功します。  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 プロシージャにパラメーターがありません。  
  
 この手順は、アプライアンスのトラフィックが少ない場合に使用する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定データベースロールまたは**CONTROL SERVER**権限のメンバーシップが必要です。  
  
## <a name="example"></a>例  
 次の例では、データベース暗号化キーを再生成します。  
  
```sql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_pdw_database_encryption &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
