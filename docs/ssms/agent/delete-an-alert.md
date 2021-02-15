---
title: Delete an Alert
description: Delete an Alert
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], deleting
- deleting alerts
- canceling alerts
- dropping alerts
- disabling alerts
- removing alerts
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 02/04/2021
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: bf4cefa3d6bcd307b80ae4f4dc0944cdb18bcdba
ms.sourcegitcommit: 0b400bb99033f4b836549cb11124a1f1630850a1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2021
ms.locfileid: "99978789"
---
# <a name="delete-an-alert"></a>Delete an Alert

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

この記事では、SQL Server Management Studio または Transact-SQL を使用して Microsoft SQL Server エージェントの警告を削除する方法について説明します。

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始する前に

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>制限事項と制約事項

警告を削除すると、この警告に関連するすべての通知も削除されます。

### <a name="security"></a><a name="Security"></a>セキュリティ

#### <a name="permissions"></a><a name="Permissions"></a>アクセス許可

既定では、警告を削除できるのは、 **sysadmin** 固定サーバー ロールのメンバーだけです。  

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio の使用

### <a name="to-delete-an-alert"></a>警告を削除するには

1. **オブジェクト エクスプローラー** で、削除する SQL Server エージェントの警告を含むサーバーを、プラス記号を選択して展開します。

2. プラス記号を選択して **[SQL Server エージェント]** を展開します。

3. プラス記号を選択して **[警告]** フォルダーを展開します。

4. 削除する警告を右クリックして、 **[削除]** を選択します。

5. **[オブジェクトの削除]** ダイアログ ボックスで、正しい警告が選択されていることを確認し、 **[OK]** を選択します。

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL の使用

### <a name="to-delete-an-alert"></a>警告を削除するには

1. **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。

2. 標準バーで、 **[新しいクエリ]** を選択します。  

3. 次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** を選択します。

    ```
    -- deletes the SQL Server Agent alert called 'Test Alert.'
    USE msdb ;
    GO
  
    EXEC dbo.sp_delete_alert
       @name = N'Test Alert' ;
    GO
    ```

詳細については、「 [sp_delete_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)」を参照してください。
