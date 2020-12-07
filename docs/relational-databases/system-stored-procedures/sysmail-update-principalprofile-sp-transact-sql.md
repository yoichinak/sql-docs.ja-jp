---
description: sysmail_update_principalprofile_sp (Transact-SQL)
title: sysmail_update_principalprofile_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bba3f6ca7046825f4bdd13e062b67b554b636405
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492822"
---
# <a name="sysmail_update_principalprofile_sp-transact-sql"></a>sysmail_update_principalprofile_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プリンシパルとプロファイルの関連付けに関する情報を更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>引数  
`[ @principal_id = ] principal_id` 関連付けを変更する **msdb** データベースのデータベースユーザーまたはロールの ID。 *principal_id* は **int**,、既定値は NULL です。 *Principal_id*または*principal_name*のいずれかを指定する必要があります。  
  
`[ @principal_name = ] 'principal_name'` 関連付けを更新する **msdb** データベースのデータベースユーザーまたはロールの名前。 *principal_name* は **sysname**,、既定値は NULL です。 *Principal_id*または*principal_name*のいずれかを指定できます。  
  
`[ @profile_id = ] profile_id` 関連付けを変更するプロファイルの id。 *profile_id* は **int**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` 関連付けを変更するプロファイルの名前。 *profile_name* は **sysname**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定する必要があります。  
  
`[ @is_default = ] 'is_default'` このプロファイルが、データベースユーザーの既定のプロファイルかどうかを指定します。 データベースユーザーは、既定のプロファイルを1つだけ持つことができます。 *is_default* は **ビット**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 このストアド プロシージャでは、指定したプロファイルを、データベース ユーザーの既定のプロファイルにするかどうかを変更します。 データベース ユーザーが持つことのできる既定のプライベート プロファイルは 1 つだけです。  
  
 アソシエーションのプリンシパル名が **public** の場合、またはアソシエーションのプリンシパル id が **0**の場合、このストアドプロシージャはパブリックプロファイルを変更します。 既定のパブリック プロファイルは 1 つしか存在できません。  
  
 ** \@ Is_default**が '**1**' で、プリンシパルが複数のプロファイルに関連付けられている場合、指定されたプロファイルはプリンシパルの既定のプロファイルになります。 以前既定のプロファイルであったプロファイルは引き続きプリンシパルに関連付けられていますが、既定のプロファイルではなくなりました。  
  
 ストアドプロシージャ **sysmail_update_principalprofile_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 **A. プロファイルをデータベースの既定のパブリック プロファイルに設定する**  
  
 次の例では、プロファイル `General Use Profile` を、 **msdb** データベースのユーザーの既定のパブリックプロファイルに設定します。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B. プロファイルをユーザーの既定のプライベート プロファイルに設定する**  
  
 次の例では、プロファイル `AdventureWorks Administrator` を、 `ApplicationUser` **msdb** データベース内のプリンシパルの既定のプロファイルに設定します。 このプロファイルはプリンシパルに既に関連付けられている必要があります。 以前既定のプロファイルであったプロファイルは引き続きプリンシパルに関連付けられていますが、既定のプロファイルではなくなりました。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
