---
description: sp_vupgrade_replication (Transact-sql)
title: sp_vupgrade_replication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 76af37a788db667d1fc7e39976a63d04feb72a29
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547849"
---
# <a name="sp_vupgrade_replication-transact-sql"></a>sp_vupgrade_replication (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  レプリケーションサーバーをアップグレードするときに、セットアップによってアクティブ化されます。 は、現在の製品レベルでレプリケーションをサポートするために、必要に応じてスキーマとシステムデータをアップグレードします。 また、システム データベースとユーザー データベースに、新しいレプリケーション システム オブジェクトを作成します。 このストアドプロシージャは、レプリケーションのアップグレードが行われるコンピューターで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>引数  
`[ @login = ] 'login'` ディストリビューションデータベースに新しいシステムオブジェクトを作成するときに使用するシステム管理者のログインを示します。 *login* のデータ型は **sysname** で、既定値は NULL です。 *Security_mode*が Windows 認証である**1**に設定されている場合、このパラメーターは必要ありません。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンへのアップグレードの場合、このパラメーターは無視されます。  
  
`[ @password = ] 'password'` ディストリビューションデータベースに新しいシステムオブジェクトを作成するときに使用するシステム管理者のパスワードを入力します。 *パスワード* は **sysname**,、既定値は **' '** (空の文字列)。 *Security_mode*が Windows 認証である**1**に設定されている場合、このパラメーターは必要ありません。  
  
> [!NOTE]  
>  SQL 以降のバージョンにアップグレードする場合、このパラメーターは無視され [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ます。  
  
`[ @ver_old = ] 'old_version'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 このストアドプロシージャは非推奨とされており、の将来のリリースで削除される予定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。  
  
`[ @force_remove = ] 'force_removal'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @security_mode = ] 'security_mode'` ディストリビューションデータベースに新しいシステムオブジェクトを作成するときに使用するログインセキュリティモードを示します。 *security_mode* の部分は **bit** で、既定値は **0**です。 **0**の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が使用されます。 **1**の場合、Windows 認証が使用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンへのアップグレードの場合、このパラメーターは無視されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_vupgrade_replication** は、すべての種類のレプリケーションをアップグレードするときに使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_vupgrade_replication**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [レプリケートされたデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
