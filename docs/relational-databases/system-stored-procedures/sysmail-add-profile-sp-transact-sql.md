---
description: sysmail_add_profile_sp (Transact-SQL)
title: sysmail_add_profile_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 904a6898bf3791a98d64228b85939275ad5c8548
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547251"
---
# <a name="sysmail_add_profile_sp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  新しいデータベースメールプロファイルを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_name = ] 'profile\_name'` 新しいプロファイルの名前。 *profile_name* は **sysname**であり、既定値はありません。  
 
   > [!NOTE]
   > Azure SQL Managed Instance SQL エージェントを使用するプロファイル名を呼び出す必要があり **AzureManagedInstance_dbmail_profile**
  
`[ @description = ] 'description'` 新しいプロファイルの説明です (省略可能)。 *説明* は **nvarchar (256)**,、既定値はありません。  
  
`[ @profile_id = ] _new\_profile\_id OUTPUT` 新しいプロファイルの ID を返します。 *new_profile_id* は **int**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 データベースメールプロファイルには、任意の数のデータベースメールアカウントが保持されます。 データベース メールのストアド プロシージャでは、このプロシージャで生成されたプロファイル名またはプロファイル ID によって、プロファイルを参照できます。 アカウントをプロファイルに追加する方法の詳細については、「 [sysmail_add_profileaccount_sp &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)」を参照してください。  
  
 プロファイルの名前と説明はストアドプロシージャ **sysmail_update_profile_sp**で変更できますが、プロファイル id はプロファイルの有効期間中は一定のままです。  
  
 プロファイル名は Microsoft に対して一意である必要があり [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ます。または、ストアドプロシージャからエラーが返されます。  
  
 ストアドプロシージャ **sysmail_add_profile_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 **A. 新しいプロファイルを作成する**  
  
 次の例では、`AdventureWorks Administrator` という新しいデータベース メール プロファイルを作成します。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B. 新しいプロファイルを作成し、プロファイル ID を変数に格納する**  
  
 次の例では、`AdventureWorks Administrator` という新しいデータベース メール プロファイルを作成します。 この例では、プロファイル id 番号を変数に格納 `@profileId` し、新しいプロファイルのプロファイル id 番号を含む結果セットを返します。  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントを作成する](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [データベースメール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
