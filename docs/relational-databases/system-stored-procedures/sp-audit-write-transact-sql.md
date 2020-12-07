---
description: sp_audit_write (Transact-SQL)
title: sp_audit_write (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_audit_write
- sp_audit_write_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_audit_write
ms.assetid: 4c523848-1ce6-49ad-92b3-e0e90f24f1c2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 56795d7ed3da83dff9f50d70f639300dae0da3a1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536714"
---
# <a name="sp_audit_write-transact-sql"></a>sp_audit_write (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ユーザー定義の監査イベントを **USER_DEFINED_AUDIT_GROUP**に追加します。 **USER_DEFINED_AUDIT_GROUP**が有効になっていない場合、 **sp_audit_write**は無視されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_audit_write [ @user_defined_event_id = ] user_defined_event_id
    [ , [ @succeeded = ] succeeded ]
    [ , [ @user_defined_information = ] 'user_defined_information' ]
    [ ; ]
```  
  
## <a name="arguments"></a>引数  
 `[ @user_defined_event_id = ] user_defined_event_id`  
 ユーザーによって定義され、監査ログの **user_defined_event_id** 列に記録されるパラメーター。 * \@ user_defined_event_id*型は**smallint**です。  
  
 `[ @succeeded = ] succeeded`  
 イベントが成功したかどうかを示すためにユーザーによって渡されるパラメーター。 これは、監査ログの succeeded 列に表示されます。 `@succeeded`**ビット**です。  
  
 `[ @user_defined_information = ] 'user_defined_information'`  
 ユーザーによって定義され、監査ログの新しい user_defined_event_id 列に記録されるテキストです。 `@user_defined_information`**nvarchar (4000)** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
 失敗の原因となるのは、正しくない入力パラメーターや、監査ログへの書き込みのエラーです。  
  
## <a name="remarks"></a>解説  
 **USER_DEFINED_AUDIT_GROUP**がサーバー監査の仕様またはデータベース監査の仕様のいずれかに追加されると、 **sp_audit_write**によってトリガーされたイベントが監査ログに含まれます。  
  
## <a name="permissions"></a>アクセス許可  
 **Public**データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-creating-a-user-defined-audit-event-with-informational-text"></a>A. 情報テキストを含むユーザー定義の監査イベントを作成する  
 次の例では、id が27で、succeeded の値が0で、オプションの情報テキストを含む監査イベントを作成します。  
  
```  
EXEC sp_audit_write @user_defined_event_id =  27 ,   
              @succeeded =  0   
            , @user_defined_information = N'Access to a monitored object.' ;  
```  
  
### <a name="b--creating-a-user-defined-audit-event-without-informational-text"></a>B.  ユーザー定義の監査イベントを情報テキストなしで作成する  
 次の例では、ID が 27、成功時の値が 0 で、オプションの情報テキストまたはオプションのパラメーター名を含まない監査イベントを作成します。  
  
```  
EXEC sp_audit_write 27, 0;  
  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
