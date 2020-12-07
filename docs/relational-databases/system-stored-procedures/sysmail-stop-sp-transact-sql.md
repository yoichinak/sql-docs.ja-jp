---
description: sysmail_stop_sp (Transact-SQL)
title: sysmail_stop_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_stop_sp_TSQL
- sysmail_stop_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_stop_sp
ms.assetid: 045ee36f-5bf0-4626-b5ee-e84db06ce16f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6630ddcb05645422ba2049636637a3e480e543c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473350"
---
# <a name="sysmail_stop_sp-transact-sql"></a>sysmail_stop_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  外部プログラムが使用しているオブジェクトを停止することによって、データベースメールを停止 [!INCLUDE[ssSB](../../includes/sssb-md.md)] します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_stop_sp  
```  
  
## <a name="arguments"></a>引数  
 None  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 このストアドプロシージャは **msdb** データベースにあります。  
  
 このストアドプロシージャは、送信メッセージ要求を保持するデータベースメールキューを停止し、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 外部プログラムのアクティブ化をオフにします。  
  
 キューが停止されると、データベースメール外部プログラムはメッセージを処理しません。 このストアド プロシージャを使用すると、トラブルシューティングやメンテナンスの目的でデータベース メールを停止できます。  
  
 データベースメールを開始するには、 **sysmail_start_sp**を使用します。 オブジェクトが停止しても、 **sp_send_dbmail** はメールを受け取ることに注意 [!INCLUDE[ssSB](../../includes/sssb-md.md)] してください。  
  
> [!NOTE]  
>  このストアドプロシージャは、データベースメールのキューのみを停止します。 このストアドプロシージャは [!INCLUDE[ssSB](../../includes/sssb-md.md)] 、データベースでのメッセージ配信を非アクティブ化しません。 このストアドプロシージャでは、データベースメール拡張ストアドプロシージャを無効にして、セキュリティでセキュリティを低下させることはできません。 拡張ストアドプロシージャを無効にするには、 **sp_configure**システムストアドプロシージャの[データベースメール XPs オプション](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、 **msdb** データベースのデータベースメールを停止します。 この例では、データベースメールが有効になっていることを前提としています。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_stop_sp ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_start_sp &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
