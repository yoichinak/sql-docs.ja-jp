---
description: sp_changeobjectowner (Transact-sql)
title: sp_changeobjectowner (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e96c93be7b21deb0966e0a48f5fde3258501ac6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464426"
---
# <a name="sp_changeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベース内のオブジェクトの所有者を変更します。  
  
> [!IMPORTANT]
>  このストアドプロシージャは、で使用可能なオブジェクトに対してのみ機能 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] します。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md) または [alter AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) を使用してください。 **sp_changeobjectowner** によってスキーマと所有者の両方が変更されます。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との互換性を維持するために、現在の所有者と新しい所有者がデータベースのユーザー名と同じ名前のスキーマを所有している場合は、このストアド プロシージャはオブジェクトの所有者だけを変更します。  
> 
> [!IMPORTANT]
>  このストアド プロシージャには、新しい権限要件が追加されています。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'object'` 現在のデータベース内の既存のテーブル、ビュー、ユーザー定義関数、またはストアドプロシージャの名前を指定します。 *オブジェクト* は **nvarchar (776)**,、既定値はありません。 *オブジェクト*は、 _existing_owner_の形式で、既存のオブジェクトの所有者で修飾でき**ます。** スキーマとその所有者の名前が同じである場合は、_オブジェクト_。  
  
`[ @newowner = ] 'owner_ '` オブジェクトの新しい所有者となるセキュリティアカウントの名前を指定します。 *owner* は **sysname**,、既定値はありません。 *所有者* は、現在のデータベースにアクセスできる有効なデータベースユーザー、サーバーロール、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] windows ログイン、または windows グループである必要があります。 新しい所有者が、対応するデータベースレベルのプリンシパルが存在しない Windows ユーザーまたは Windows グループである場合は、データベースユーザーが作成されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changeobjectowner** オブジェクトから既存のすべてのアクセス許可を削除します。 **Sp_changeobjectowner**を実行した後も、保持するアクセス許可を再適用する必要があります。 そのため、 **sp_changeobjectowner**を実行する前に、既存のアクセス許可のスクリプトを作成することをお勧めします。 オブジェクトの所有権が変更された後、スクリプトを使用してアクセス許可を再適用できます。 権限スクリプトを実行する前に、そのスクリプトでオブジェクトの所有者を変更する必要があります。  
  
 セキュリティ保護可能なオブジェクトの所有者を変更するには、ALTER AUTHORIZATION を使用します。 スキーマを変更するには、ALTER SCHEMA を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Db_owner**固定データベースロールのメンバーシップ、または**db_ddladmin**固定データベースロールと**db_securityadmin**固定データベースロールのメンバーシップ、およびオブジェクトに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、`authors` テーブルの所有者を `Corporate\GeorgeW` に変更します。  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
