---
description: sp_dropuser (Transact-sql)
title: sp_dropuser (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropuser
- sp_dropuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropuser
ms.assetid: e28f18f9-7ecf-4568-89f4-fe5c520df386
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f44b851dc2d60899f27c8419dfdb557951043683
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536162"
---
# <a name="sp_dropuser-transact-sql"></a>sp_dropuser (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースからデータベースユーザーを削除します。 **sp_dropuser** は、以前のバージョンのと互換性が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] あります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>引数  
`[ @name_in_db = ] 'user'` 削除するユーザーの名前を指定します。 *user* は **sysname**で、既定値はありません。 *ユーザー* は現在のデータベースに存在する必要があります。 Windows ログインを指定する場合は、データベースでログインとして認識されている名前を使用してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_dropuser** は **sp_revokedbaccess** を実行して、現在のデータベースからユーザーを削除します。  
  
 現在のデータベースから削除できるユーザー名の一覧を表示するには、 **sp_helpuser** を使用します。  
  
 データベースユーザーが削除されると、そのユーザーのエイリアスもすべて削除されます。 ユーザーがユーザーと同じ名前の空のスキーマを所有している場合、スキーマは削除されます。 ユーザーがデータベース内の他の securables を所有している場合、そのユーザーは削除されません。 オブジェクトの所有権は、最初に別のプリンシパルに転送する必要があります。 詳細については、「[ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)」を参照してください。 データベースユーザーを削除すると、そのユーザーに関連付けられている権限が自動的に削除され、そのユーザーがメンバーとなっているデータベースロールから削除されます。  
  
 **sp_dropuser**を使用して、データベース所有者 (**dbo**) **INFORMATION_SCHEMA**ユーザー、または**マスター**データベースまたは**tempdb**データベースから**guest**ユーザーを削除することはできません。 システム以外のデータベースで `EXEC sp_dropuser 'guest'` は、ユーザーの **ゲスト**から CONNECT 権限が取り消されます。 ただし、ユーザー自体は削除されません。  
  
 **sp_dropuser** は、ユーザー定義のトランザクション内では実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する ALTER ANY USER 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、ユーザーを `Albert` 現在のデータベースから削除します。  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
