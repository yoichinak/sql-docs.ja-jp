---
description: sp_pdw_log_user_data_masking (Azure Synapse Analytics)
title: sp_pdw_log_user_data_masking (Azure Synapse Analytics) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c014f76aac1544e16ec693277a034779f75883cd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92255614"
---
# <a name="sp_pdw_log_user_data_masking-azure-synapse-analytics"></a>sp_pdw_log_user_data_masking (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  **Sp_pdw_log_user_data_masking**を使用して、アクティビティログでユーザーデータのマスキングを有効に [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] します。 ユーザーデータのマスキングは、アプライアンス上のすべてのデータベースのステートメントに影響します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] **Sp_pdw_log_user_data_masking**によって影響を受けるアクティビティログは、特定の [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] アクティビティログです。 **sp_pdw_log_user_data_masking** は、データベーストランザクションログまたはエラーログには影響しません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **背景:** 既定の構成 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] アクティビティログには完全なステートメントが含まれ [!INCLUDE[tsql](../../includes/tsql-md.md)] ており、場合によっては **INSERT**、 **UPDATE**、 **SELECT** ステートメントなどの操作に含まれるユーザーデータが含まれます。 アプライアンスで問題が発生した場合は、問題の原因となった状況を分析して問題を再現する必要がありません。 ユーザーデータがアクティビティログに書き込まれないようにするには [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 、このストアドプロシージャを使用してユーザーデータのマスキングを有効にすることを選択できます。 ステートメントは引き続きアクティビティログに書き込まれます [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] が、ユーザーデータを含む可能性のあるステートメント内のすべてのリテラルはマスクされ、いくつかの定義済みの定数値に置き換えられます。  
  
 アプライアンスで transparent data encryption を有効にすると、アクティビティログ内のユーザーデータのマスキングが自動的に有効になり [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

#### <a name="parameters"></a>パラメーター  
`[ @masking_mode = ] masking_mode` 透過的なデータ暗号化ログユーザーデータのマスキングが有効かどうかを指定します。 *masking_mode* は **int**,、値は次のいずれかを指定することができます。  
  
-   0 = 無効。ユーザーデータはアクティビティログに表示され [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。  
  
-   1 = 有効になっていると、ユーザーデータステートメントはアクティビティログに表示され [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ますが、ユーザーデータはマスクされます。  
  
-   2 = ユーザーデータを含むステートメントは、アクティビティログには書き込まれません [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。  
  
 パラメーターを指定せずに **sp_pdw_ log_user_data_masking** を実行すると、アプライアンス上の tde ログユーザーデータマスクの現在の状態がスカラー結果セットとして返されます。  
  
## <a name="remarks"></a>解説  
 ユーザーデータのマスキング [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] アクティビティログでは、ユーザーデータを含めることができる **SELECT** ステートメントと DML ステートメントで、定義済みの定数値を持つリテラルを置換できます。 *Masking_mode*を1に設定しても、列名やテーブル名などのメタデータはマスクされません。 *Masking_mode*を2に設定すると、列名やテーブル名などのメタデータを含むステートメントが削除されます。  
  
 アクティビティログでのユーザーデータのマスキング [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] は、次のように実装されます。  
  
-   既定では、アクティビティログの TDE とユーザーデータのマスキング [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] はオフになっています。 アプライアンスでデータベース暗号化が有効になっていない場合、ステートメントは自動的にマスクされません。  
  
-   アプライアンスで TDE を有効にすると、アクティビティログのユーザーデータのマスキングが自動的にオンになり [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。  
  
-   TDE を無効にしても、アクティビティログでのユーザーデータのマスキングには影響しません [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。  
  
-   [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] **Sp_pdw_log_user_data_masking**の手順を使用して、アクティビティログでユーザーデータのマスキングを明示的に有効にすることができます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定データベースロールまたは**CONTROL SERVER**権限のメンバーシップが必要です。  
  
## <a name="example"></a>例  
 次の例では、TDE のログユーザーデータのマスキングを有効にします。  
  
```sql  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>参照  
 [sp_pdw_database_encryption &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
