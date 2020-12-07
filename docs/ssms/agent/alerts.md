---
description: 警告
title: 警告
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, event types
- SQL Server Agent alerts, names
- alerts [SQL Server], performance conditions
- alerts [SQL Server], about alerts
- WMI event responses [SQL Server Agent alerts]
- events [WMI]
- performance condition alerts [SQL Server Agent]
- alerts [SQL Server], event types
- SQL Server Agent alerts, performance conditions
- SQL Server Agent alerts, about alerts
- alerts [SQL Server], names
ms.assetid: 3f57d0f0-4781-46ec-82cd-b751dc5affef
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ea3cc85669b31eed9ba2b91d6d4c91c8b59bd603
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039226"
---
# <a name="alerts"></a>警告

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

イベントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって生成され、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows アプリケーション ログに記録されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、アプリケーション ログを読み取り、そこに書き込まれているイベントを、定義済みの警告と比較します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって一致が検出されると、イベントに対する自動応答である警告を発します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントの監視だけでなく、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントはパフォーマンス状態および Windows Management Instrumentation (WMI) イベントも監視します。  
  
警告を定義するには、次の項目を指定します。  
  
-   警告の名前を指定します。  
  
-   警告をトリガーするイベントまたはパフォーマンス状態  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがそのイベントまたはパフォーマンス状態への応答として実行するアクション  
  
## <a name="naming-an-alert"></a>警告の命名  
すべての警告に名前を付ける必要があります。 警告名は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意である必要があります。使用できる文字数は最大 **128** 文字です。  
  
## <a name="selecting-an-event-type"></a>イベントの種類の選択  
警告は特定の種類のイベントに応答します。 警告は次のイベントの種類に応答します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベント  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス状態  
  
-   WMI イベント  
  
イベントの種類によって、イベントの詳細を指定するために使用するパラメーターが異なります。  
  
## <a name="specifying-a-sql-server-event"></a>SQL Server イベントの指定  
1 つ以上のイベントに応答して発生する警告を指定できます。 次のパラメーターを使用して警告をトリガーするイベントを指定します。  
  
-   **エラー番号**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、特定のエラーが発生したときに警告を発します。 たとえば、データベース コンソール コマンド (DBCC) の不正な起動試行に対する応答をエラー番号 2571 と指定できます。  
  
-   **重大度レベル**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、特定の重大度のエラーが発生したときに警告を発します。 たとえば、Transact-SQL ステートメントでの構文エラーに重大度 15 を指定できます。  
  
-   **[データベース]**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、特定のデータベースでイベントが発生した場合のみ警告を発します。 このオプションは、エラー番号または重大度に加えて適用できます。 たとえば、1 つのインスタンスで運用データベースとレポート用データベースを使用している場合、運用データベースで構文エラーが発生した場合のみ、警告を発するように定義できます。  
  
-   **イベント テキスト**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、指定されたイベントのイベント メッセージに特定の文字列が含まれている場合に警告を発します。 たとえば、特定のテーブル名または特定の定数を含んでいるメッセージに応答する警告を定義できます。  
  
## <a name="selecting-a-performance-condition"></a>パフォーマンス状態の選択  
特定のパフォーマンス状態に応答する警告を指定できます。 この場合、監視するパフォーマンス カウンター、警告を発生するしきい値、および警告発生時にカウンターが示す動作を指定します。 パフォーマンス状態を設定するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの **[新しい警告]** または **[警告のプロパティ]** ダイアログ ボックスを開き、 **[全般]** ページで次の項目を定義する必要があります。  
  
-   **Object**  
  
    オブジェクトは、監視されるパフォーマンスの領域です。  
  
-   **カウンター**  
  
    カウンターは、監視される領域の属性です。  
  
-   **インスタンス**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでは、監視する属性に特定のインスタンスがある場合、そのインスタンスを定義します。  
  
-   **[警告カウンター]** および **[値]**  
  
    警告およびそれを生成する動作のしきい値です。 しきい値は数値です。 動作は、 **[設定値未満]** 、 **[設定値に等しい]** 、 **[設定値を超える]** のいずれかになります。 **[値]** は、パフォーマンス状況の警告カウンターの基準となる数値です。 たとえば、パフォーマンス オブジェクト **SQLServer:Locks** で、 **Lock Wait Time** が 30 分を超えると警告が発生するように設定するには、 **[設定値を超える]** を選択し、 **[値] を 30 に指定**します。  
  
    別の例として、 **tempdb** の空き領域が 1,000 KB を下回った場合にパフォーマンス オブジェクト **SQLServer:Transactions** に対して警告が発生するように指定できます。 このように設定するには、カウンター **[Free space in tempdb (KB)]** を選択し **[設定値未満]** を選択します。さらに、 **[値]** を **1000**に設定します。  
  
    > [!NOTE]  
    > パフォーマンス データは定期的にサンプリングされます。したがって、しきい値に達してからパフォーマンス警告が発せられるまでの間にわずかな遅延 (数秒) が生じる可能性があります。  
  
    > [!NOTE]  
    > サーバー名を格納するイベント ログ変数は、32 文字までに制限されています。 したがって、ホスト名とインスタンス名の合計サイズが 32 文字を超えると、次のエラーが表示されることがあります。
    
   ``` 
   Warning,[466] Failed to copy server name LONGNAMESQLSERV\LONGINSTANCENAME while generating performance counter alerts.
   ```
  
  
## <a name="selecting-a-wmi-event"></a>WMI イベントの選択  
特定の WMI イベントに応答して警告が発生するように指定できます。 WMI イベントを選択するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの **[新しい警告]** または **[警告のプロパティ]** ダイアログ ボックスを開き、 **[全般]** ページで次の項目を定義する必要があります。  
  
-   **Namespace**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを WMI クライアントとして、イベントをクエリするために用意された WMI 名前空間に登録します。  
  
-   **クエリ**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、Windows Management Instrumentation Query Language (WQL) ステートメントを使用して、特定のイベントを識別します。  
  
一般的なタスクへのリンクは次のとおりです。  
  
**メッセージ番号に基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**重大度レベルに基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**WMI イベントに基づいた警告を作成するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-a-wmi-event-alert.md)  
  
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
[sp_update_alert (Transact-SQL)](../../relational-databases/performance-monitor/use-sql-server-objects.md)  
