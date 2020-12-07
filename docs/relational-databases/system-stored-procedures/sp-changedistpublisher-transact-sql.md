---
description: sp_changedistpublisher (Transact-sql)
title: sp_changedistpublisher (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ca2b3369a75d2e2b80624d99d2fe11459b8ff749
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548268"
---
# <a name="sp_changedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  ディストリビューション パブリッシャーのプロパティを変更します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値はありません。  
  
`[ @property = ] 'property'` 指定されたパブリッシャーに対して変更するプロパティを指定します。 *プロパティ* は **sysname** で、次のいずれかの値を指定できます。  
  
`[ @value = ] 'value'` 指定されたプロパティの値です。 *値* は **nvarchar (255)**,、既定値は NULL です。  
  
`[ @storage_connection_string = ] 'storage_connection_string'` SQL Managed Instance には、Azure SQL Database ストレージボリュームのアクセスキーと一致する必要があります。 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 次の表に、パブリッシャーのプロパティと、それぞれの値を示します。  
  
|プロパティ|値|説明|  
|--------------|------------|-----------------|  
|**active**|**true**|パブリッシャーをアクティブにします。|  
||**false**|パブリッシャーを非アクティブ化します。|  
|**distribution_db**||ディストリビューションデータベースの名前。|  
|**ログイン**||ログイン名。|  
|**password**||指定されたログインの強力なパスワード。|  
|**security_mode**|**1**|パブリッシャーに接続するときに Windows 認証を使用。 *これは、以外* [!INCLUDE[msCoName](../../includes/msconame-md.md)] のでは変更できません。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*パブリッシャー。*|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーに接続するときに認証を使用します。 *これは、以外* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のでは変更できません。*パブリッシャー。*|  
|**working_directory**||パブリケーションのデータおよびスキーマ ファイルを保存するために使用する作業ディレクトリです。|  
|NULL (既定値)||使用可能なすべての *プロパティ* オプションが印刷されます。| 
|**storage_connection_string**| アクセス キー | データベースが Azure SQL Managed Instance の場合の作業ディレクトリのアクセスキー。 
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changedistpublisher** は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changedistpublisher**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
