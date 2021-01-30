---
description: sp_helplogins (Transact-SQL)
title: sp_helplogins (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b58e74a30ddd86fc2edbfc8db553ddf9449181db
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99183124"
---
# <a name="sp_helplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  各データベース内のログインと、それらに関連付けられているユーザーに関する情報を提供します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @LoginNamePattern = ] 'login'` ログイン名を指定します。 *login* のデータ型は **sysname** で、既定値は NULL です。 指定した場合、*ログイン* が存在する必要があります。 *Login* が指定されていない場合は、すべてのログインに関する情報が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 最初のレポートには、次の表に示すとおり、指定した各ログインに関する情報が含まれます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|ログイン名。|  
|**SID**|**varbinary(85)**|ログインセキュリティ識別子 (SID)。|  
|**DefDBName**|**sysname**|のインスタンスに接続するときに、 **loginが** 使用する既定のデータベース [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。|  
|**DefLangName**|**sysname**|**ログイン** で使用される既定の言語。|  
|**Auser**|**char (5)**|はい = データベースにユーザー名が関連付けられ **ています** 。<br /><br /> No = **ログイン** には、関連付けられたユーザー名がありません。|  
|**ARemote**|**char (7)**|はい = **ログイン** に関連付けられているリモートログインです。<br /><br /> No = **loginlogin** には、関連付けられたログインがありません。|  
  
 2 番目のレポートには、次の表に示すとおり、各ログインにマップされているユーザーに関する情報、およびログインのロール メンバーシップが含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|ログイン名。|  
|**DBName**|**sysname**|のインスタンスに接続するときに、 **loginが** 使用する既定のデータベース [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。|  
|**UserName**|**sysname**|の場合、このユーザーアカウントは、 **dbname** でに **マップされ**、その **ログイン** が **dbname** のメンバーであるロールです。|  
|**UserOrAlias**|**char (8)**|MemberOf = **UserName** はロールです。<br /><br /> User = **UserName** はユーザーアカウントです。|  
  
## <a name="remarks"></a>コメント  
 ログインを削除する前に、 **sp_helplogins** を使用して、ログインにマップされているユーザーアカウントを特定します。  
  
## <a name="permissions"></a>アクセス許可  
 **Securityadmin** 固定サーバーロールのメンバーシップが必要です。  
  
 特定のログインにマップされているすべてのユーザーアカウントを識別するには、 **sp_helplogins** サーバー内のすべてのデータベースを確認する必要があります。 このため、サーバー上の各データベースについて、次の条件の少なくとも1つが true である必要があります。  
  
-   **Sp_helplogins** を実行しているユーザーには、データベースにアクセスする権限があります。  
  
-   データベースで **guest** ユーザーアカウントが有効になっています。  
  
 **Sp_helplogins** がデータベースにアクセスできない場合、 **sp_helplogins** は可能な限り多くの情報を返し、エラーメッセージ15622を表示します。  
  
## <a name="examples"></a>例  
 次の例では、ログインに関する情報を報告し `John` ます。  
  
```  
EXEC sp_helplogins 'John';  
GO  
  
LoginName SID                        DefDBName DefLangName AUser ARemote   
--------- -------------------------- --------- ----------- ----- -------   
John      0x23B348613497D11190C100C  master    us_english  yes   no  
  
(1 row(s) affected)  
  
LoginName   DBName   UserName   UserOrAlias   
---------   ------   --------   -----------   
John        pubs     John       User          
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
