---
description: MOVE CONVERSATION (Transact-SQL)
title: MOVE CONVERSATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs:
- TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 221c16ac567c7dfffa86d2c2259bd86d62cc1d8a
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91498100"
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  メッセージ交換を、別のメッセージ交換グループに移動します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *conversation_handle*  
 移動するメッセージ交換のメッセージ交換ハンドルを含む、変数または定数。 *conversation_handle* は型 **uniqueidentifier** にする必要があります。  
  
 TO *conversation_group_id*  
 メッセージ交換の移動先となるメッセージ交換グループの識別子を含む、変数または定数。 *conversation_group_id* は型 **uniqueidentifier** にする必要があります。  
  
## <a name="remarks"></a>注釈  
 MOVE CONVERSATION ステートメントは、*conversation_handle* で指定されたメッセージ交換を、*conversation_group_id* で識別されるメッセージ交換グループに移動します。 同じキューに関連付けられているメッセージ交換グループ間でのみ、ダイアログをリダイレクトできます。  
  
> [!IMPORTANT]  
>  MOVE CONVERSATION ステートメントがバッチまたはストアド プロシージャで最初のステートメントではない場合は、前のステートメントの後に、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのターミネータであるセミコロン (**;**) を指定する必要があります。  
  
 MOVE CONVERSATION ステートメントは、ステートメントを含むトランザクションがコミットまたはロールバックされるまで、*conversation_handle* に関連付けられているメッセージ交換グループ、および *conversation_group_id* で指定されたメッセージ交換グループをロックします。  
  
 ユーザー定義の関数では、MOVE CONVERSATION は無効です。  
  
## <a name="permissions"></a>アクセス許可  
 メッセージ交換を移動するには、そのメッセージ交換およびメッセージ交換グループの所有者であるか、固定サーバー ロール sysadmin または固定データベース ロール db_owner のメンバーである必要があります。  
  
## <a name="examples"></a>例  
 次の例では、メッセージ交換を別のメッセージ交換グループに移動します。  
  
```sql  
DECLARE @conversation_handle UNIQUEIDENTIFIER,  
        @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_handle =  
    <retrieve conversation handle from database> ;  
SET @conversation_group_id =  
    <retrieve conversation group ID from database> ;  
  
MOVE CONVERSATION @conversation_handle TO @conversation_group_id ;  
```  
  
## <a name="see-also"></a>関連項目  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
