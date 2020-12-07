---
description: sp_addapprole (Transact-sql)
title: sp_addapprole (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addapprole_TSQL
- sp_addapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fa68e8b0d965fae3a1c27f5ca2705bc003d7b616
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481555"
---
# <a name="sp_addapprole-transact-sql"></a>sp_addapprole (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  アプリケーション ロールを現在のデータベースに追加します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>引数  
`[ @rolename = ] 'role'` 新しいアプリケーションロールの名前を指定します。 *role* の型は **sysname**で、既定値はありません。 *ロール* は有効な識別子である必要があり、現在のデータベースに存在することはできません。  
  
 アプリケーションロールの名前には、文字、記号、数字など、1 ~ 128 文字までを含めることができます。 ロール名に円記号 () を含め \\ たり、NULL や空の文字列 (' ') を含めたりすることはできません。  
  
`[ @password = ] 'password'` アプリケーションロールをアクティブ化するために必要なパスワードを指定します。 *パスワード* は **sysname**,、既定値はありません。 *パスワード* を NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 以前のバージョンので [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、ユーザー (およびロール) はスキーマと完全に区別されていませんでした。 以降 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では、スキーマはロールと完全に区別されています。 この新しいアーキテクチャは CREATE APPLICATION ROLE の動作に反映されています。 このステートメントは **sp_addapprole**を置き換えます。  
  
 以前のバージョンのとの下位互換性を維持するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **sp_addapprole** は次の操作を実行します。  
  
-   アプリケーション ロールと同じ名前のスキーマが存在しない場合、同じ名前のスキーマが作成されます。 新しいスキーマはアプリケーションロールによって所有され、アプリケーションロールの既定のスキーマになります。  
  
-   アプリケーションロールと同じ名前のスキーマが既に存在する場合、プロシージャは失敗します。  
  
-   パスワードの複雑さは、 **sp_addapprole**によってチェックされません。 ただし、CREATE APPLICATION ROLE では確認されます。  
  
 パラメーターの *パスワード* は、一方向のハッシュとして格納されます。  
  
 **Sp_addapprole**ストアドプロシージャは、ユーザー定義のトランザクション内から実行することはできません。  
  
> [!IMPORTANT]  
>  Microsoft ODBC **encrypt** オプションは、 **SqlClient**ではサポートされていません。 可能な場合は、アプリケーション ロールの資格情報の入力を求めるメッセージを実行時に表示してください。 資格情報をファイルに保存するのは避けてください。 資格情報を保持する必要がある場合は、CryptoAPI 関数を使用して暗号化します。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する ALTER ANY APPLICATION ROLE 権限が必要です。 新しいロールと同じ名前および同じ所有者のスキーマが存在しない場合は、そのデータベースに対する CREATE SCHEMA 権限も必要です。  
  
## <a name="examples"></a>例  
 次の例では、パスワードを持つ新しいアプリケーションロールを `SalesApp` `x97898jLJfcooFUYLKm387gf3` 現在のデータベースに追加します。  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
