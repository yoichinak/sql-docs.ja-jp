---
description: sp_pdw_database_encryption (Azure Synapse Analytics)
title: sp_pdw_database_encryption (Azure Synapse Analytics) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f8d77853846a18bd310d8afa58101cf66a24475b
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92258088"
---
# <a name="sp_pdw_database_encryption-azure-synapse-analytics"></a>sp_pdw_database_encryption (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  **Sp_pdw_database_encryption**を使用して、アプライアンスに対して透過的なデータ暗号化を有効にし [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。 **Sp_pdw_database_encryption**を1に設定した場合は、 **ALTER database**ステートメントを使用して、tde を使用してデータベースを暗号化します。  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

#### <a name="parameters"></a>パラメーター  
`[ @enabled = ] enabled` 透過的なデータ暗号化が有効かどうかを判断します。 *有効な* は **int**で、次のいずれかの値を指定できます。  
  
-   0 = 無効  
  
-   1 = 有効  
  
 パラメーターを指定せずに **sp_pdw_database_encryption** を実行すると、アプライアンス上の tde の現在の状態がスカラー結果セットとして返されます (無効の場合は0、有効の場合は 1)。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **Sp_pdw_database_encryption**を使用して tde を有効にすると、tempdb データベースが削除、再作成、および暗号化されます。 そのため、別のアクティブなセッションが tempdb を使用しているときに、アプライアンスで TDE を有効にすることはできません。 アプライアンスで TDE を有効または無効にする操作は、アプライアンスの状態を変更するアクションです。ほとんどの場合、アプライアンスの有効期間内に1回実行することが想定されており、アプライアンスにトラフィックがないときに実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定データベースロールまたは**CONTROL SERVER**権限のメンバーシップが必要です。  
  
## <a name="example"></a>例  
 次の例では、アプライアンスで TDE を有効にします。  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
