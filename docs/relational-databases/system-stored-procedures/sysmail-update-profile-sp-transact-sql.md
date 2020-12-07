---
description: sysmail_update_profile_sp (Transact-SQL)
title: sysmail_update_profile_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 78a123514e990499f191cbc6742870647adebc5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454751"
---
# <a name="sysmail_update_profile_sp-transact-sql"></a>sysmail_update_profile_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース メール プロファイルの説明または名前を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` 更新するプロファイル id。 *profile_id* は **int**,、既定値は NULL です。 少なくとも1つの *profile_id* または *profile_name* を指定する必要があります。 両方が指定されている場合、プロシージャはプロファイルの名前を変更します。  
  
`[ @profile_name = ] 'profile_name'` 更新するプロファイルの名前、またはプロファイルの新しい名前。 *profile_name* は **sysname**,、既定値は NULL です。 少なくとも1つの *profile_id* または *profile_name* を指定する必要があります。 両方が指定されている場合、プロシージャはプロファイルの名前を変更します。  
  
`[ @description = ] 'description'` プロファイルの新しい説明。 *説明* は **nvarchar (256)**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 プロファイル id とプロファイル名の両方を指定すると、プロファイルの名前が指定した名前に変更され、プロファイルの説明が更新されます。 これらの引数のいずれか1つだけを指定すると、プロファイルの説明が更新されます。  
  
 ストアドプロシージャ **sysmail_update_profile_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 **A. プロファイルの説明を変更する**  
  
 次の例では、msdb データベースのという名前のプロファイルの説明を変更し `AdventureWorks Administrator` ます。 **msdb**  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@description = 'Administrative mail profile.';  
```  
  
 **B. プロファイルの名前と説明を変更する**  
  
 次の例では、プロファイルの名前と説明をプロファイル id で変更し `750` ます。  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_id = 750  
    ,@profile_name = 'Operator'  
    ,@description = 'Profile to send alert e-mail to operators.';  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [データベースメールアカウントを作成する](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
