---
description: データベース メールから送信された電子メール メッセージの状態の確認
title: データベース メールから送信された電子メール メッセージの状態
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- e-mail [SQL Server], status information
- mail [SQL Server], status information
- Database Mail [SQL Server], message status
- status information [Database Mail]
ms.assetid: eb290f24-b52f-46bc-84eb-595afee6a5f3
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
ms.openlocfilehash: 245a50951896f923165e011fc51c09abd00f96e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421246"
---
# <a name="check-the-status-of-e-mail-messages-sent-with-database-mail"></a>データベース メールから送信された電子メール メッセージの状態の確認
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベース メール経由で送信された電子メール メッセージの状態を確認する方法について説明します。  
  
-   **作業を開始する準備:**  
  
-   **データベース メールを使用して送信された電子メールの状態を表示する方法:**  [Transact-SQL の使用](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
 データベース メールは、送信する電子メール メッセージのコピーを保持し、 **msdb**データベースの **sysmail_allitems**、 **sysmail_sentitems**、 **sysmail_unsentitems** 、および **sysmail_faileditems** の各ビューに表示します。 データベース メール外部プログラムは、利用状況をログに記録し、Windows アプリケーション イベント ログや **msdb** データベースの **sysmail_event_log** ビューでそのログを表示します。 電子メール メッセージの状態を確認するには、このビューに対してクエリを実行します。 電子メール メッセージの状態は、 **sent**、 **unsent**、 **retrying**、および **failed**のいずれかになります。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 **データベース メールを使用して送信された電子メールの状態を表示するには**  
  
1.  **sysmail_allitems** テーブルから選択して、 **mailitem_id** または **sent_status**で対象のメッセージを指定します。  
  
2.  その電子メール メッセージについてデータベース メール外部プログラムから返される状態を確認するには、次のセクションに示すように、 **mailitem_id** 列で **sysmail_allitems** と **sysmail_event_log** ビューを結合します。  
  
     データベース メール外部プログラムの既定では、正常に送信されたメッセージについての情報がログに記録されません。 すべてのメッセージをログに記録するには、 **データベース メール構成ウィザード** の **[システム パラメーターの構成]** ページを使用して、ログのレベルを詳細に設定します。  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、外部プログラムが正常に送信できなかった、 `danw` への電子メール メッセージに関する情報を表示します。 このステートメントは、件名、外部プログラムでメッセージの送信に失敗した日時、およびデータベース メール ログに記録されているエラー メッセージの一覧を表示します。  
  
```  
USE msdb ;  
GO  
  
-- Show the subject, the time that the mail item row was last  
-- modified, and the log information.  
-- Join sysmail_faileditems to sysmail_event_log   
-- on the mailitem_id column.  
-- In the WHERE clause list items where danw was in the recipients,  
-- copy_recipients, or blind_copy_recipients.  
-- These are the items that would have been sent  
-- to danw.  
  
SELECT items.subject,  
    items.last_mod_date  
    ,l.description FROM dbo.sysmail_faileditems as items  
INNER JOIN dbo.sysmail_event_log AS l  
    ON items.mailitem_id = l.mailitem_id  
WHERE items.recipients LIKE '%danw%'    
    OR items.copy_recipients LIKE '%danw%'   
    OR items.blind_copy_recipients LIKE '%danw%'  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベース メールのログ記録と監査](../../relational-databases/database-mail/database-mail-log-and-audits.md)  
  
  
