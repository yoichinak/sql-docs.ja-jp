---
description: sp_changereplicationserverpasswords (Transact-SQL)
title: sp_changereplicationserverpasswords (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0d0e07afbf3837768ac2b57e3dfaa7d0c8c0d0af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481482"
---
# <a name="sp_changereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  レプリケーション [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トポロジ内のサーバーに接続するときに、レプリケーションエージェントによって使用される Windows アカウントまたはログインのために保存されたパスワードを変更します。 通常は、サーバーで実行中のエージェントがすべて同じログインまたはアカウントを使用している場合でも、個々のエージェントごとにパスワードを変更する必要があります。 このストアド プロシージャにより、サーバーで実行中のすべてのレプリケーション エージェントが使用する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたは Windows アカウントのすべてのインスタンスに対するパスワードを変更することができます。 このストアドプロシージャは、master データベースのレプリケーショントポロジ内の任意のサーバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @login_type = ] login_type` 指定された資格情報の認証の種類を指定します。 *login_type* は **tinyint**,、既定値はありません。  
  
 **1** = Windows 統合認証  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証  
  
`[ @login = ] 'login'` 変更する Windows アカウントまたはログインの名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *ログイン* は **nvarchar (257)**,、既定値はありません。  
  
`[ @password = ] 'password'` 指定した *ログイン*用に格納する新しいパスワードを指定します。 *パスワード* は **sysname**,、既定値はありません。  
  
> [!NOTE]  
>  レプリケーション パスワードを変更したら、そのパスワードを使用する各エージェントを停止して再起動し、エージェントに対して変更を反映させる必要があります。  
  
`[ @server = ] 'server'` 格納されているパスワードを変更するサーバー接続を指定します。 *サーバー* は **sysname**で、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**ディストリビューター**|ディストリビューターへのすべてのエージェント接続。|  
|**publisher**|パブリッシャーへのすべてのエージェント接続。|  
|**サブスクライバ**|サブスクライバーへのすべてのエージェント接続。|  
|**%** 標準|レプリケーション トポロジ内のすべてのサーバーへのすべてのエージェント接続です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changereplicationserverpasswords** は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changereplicationserverpasswords**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
