---
description: ユーザー定義イベントの作成
title: ユーザー定義イベントの作成
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bf18385b89ac7af32bfde26d704880eb4e9bb300
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036670"
---
# <a name="create-a-user-defined-event"></a>ユーザー定義イベントの作成
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって定義済みのイベント以外のイベントを監視するには、ユーザー定義イベントを作成します。 また、各ユーザー定義イベントに対して重大度レベルを割り当てることもできます。  
  
> [!NOTE]  
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用中に、各ユーザー定義イベント メッセージに対して **[Windows アプリケーション イベント ログに書き込む]** オプションを選択して、そのメッセージがログに書き込まれるように設定できます。 既定では、ユーザー定義メッセージが生成された場合でも、その重大度が 19 より低い場合は [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows アプリケーション ログに送られません。 したがって、重大度が 19 より低いユーザー定義メッセージは、SQL Server エージェントの警告をトリガーしません。  
  
ユーザー定義イベントには、それぞれ一意のメッセージ番号が付けられている必要があります。 ユーザー定義イベントのメッセージ番号は、50,000 より大きくする必要があります。 イベントに対するメッセージを複数の言語で定義することもできます。 ただし、他の言語のメッセージを追加するには、 **En-US** エラー メッセージが存在している必要があります。  
  
複数言語の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境を管理する場合は、サポートされている各言語でユーザー定義メッセージを作成することをお勧めします。 たとえば、英語サーバーとドイツ語サーバーの両方で使用する新しいイベント メッセージを作成する場合、イベント番号と重大度はどちらのサーバーに対しても同じものを使用しますが、各サーバーに異なる言語を割り当ててください。  
  
次のタスクでは、ユーザー定義イベントの作成方法とイベントに応答する警告についての情報が得られます。  
  
**メッセージ番号に基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**重大度レベルに基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**警告に対する応答を定義するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)  
  
**ユーザー定義のイベント エラー メッセージを作成するには**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)  
  
**ユーザー定義のイベント エラー メッセージを変更するには**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)  
  
**ユーザー定義のイベント エラー メッセージを削除するには**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)  
  
**警告を無効にしたり、再び有効にするには**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)  
  
## <a name="see-also"></a>参照  
[sp_update_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)  
