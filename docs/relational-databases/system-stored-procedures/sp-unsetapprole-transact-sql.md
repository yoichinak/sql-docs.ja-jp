---
description: sp_unsetapprole (Transact-SQL)
title: sp_unsetapprole (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unsetapprole_TSQL
- sp_unsetapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unsetapprole
ms.assetid: 4c4033d3-1a34-4dfb-835d-e3293d1a442d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b024d959c49cfba5d2d1daeef526ac5d5a484458
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547263"
---
# <a name="sp_unsetapprole-transact-sql"></a>sp_unsetapprole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  アプリケーションロールを非アクティブ化して、以前のセキュリティコンテキストに戻します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unsetapprole @cookie   
```  
  
## <a name="arguments"></a>引数  
 **\@cookie**  
 アプリケーションロールがアクティブ化されたときに作成されたクッキーを指定します。 Cookie は [sp_setapprole &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)によって作成されます。 **varbinary (8000)**。  
  
> [!NOTE]  
>  **sp_setapprole** のクッキーの **OUTPUT** パラメーターは現在、適切な最大長である **varbinary(8000)** としてドキュメントに記載されています。 ただし、現在の実装では **varbinary(50)** を返します。 アプリケーションは、今後のリリースでクッキーの戻り値のサイズが増加した場合にアプリケーションが引き続き正常に動作するように、 **varbinary (8000)** を引き続き予約する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) と 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **Sp_setapprole**を使用してアプリケーションロールをアクティブ化した後は、ユーザーがサーバーとの接続を切断するか**sp_unsetapprole**を実行するまで、ロールはアクティブのままになります。  
  
 アプリケーションロールの概要については、「 [アプリケーションロール](../../relational-databases/security/authentication-access/application-roles.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 アプリケーションロールがアクティブ化されたときに保存された cookie の **メンバーシップとナレッジ** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="activating-an-application-role-with-a-cookie-then-reverting-to-the-previous-context"></a>Cookie を使用してアプリケーションロールをアクティブ化してから、前のコンテキストに戻す  
 次の例では、パスワード `Sales11` が設定されているアプリケーション ロール `fdsd896#gfdbfdkjgh700mM` をアクティブ化し、クッキーを作成します。 この例では、現在のユーザーの名前を返し、 **sp_unsetapprole**を実行して元のコンテキストに戻します。  
  
```  
DECLARE @cookie varbinary(8000);  
EXEC sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.   
GO   
```  
  
## <a name="see-also"></a>参照  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)  
  
  
