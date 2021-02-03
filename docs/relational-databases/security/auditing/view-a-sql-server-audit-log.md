---
title: SQL Server 監査ログの表示 | Microsoft Docs
description: SQL Server Management Studio を使用して SQL Server で SQL Server 監査ログを表示する方法について説明します。 表示するには、CONTROL SERVER 権限が必要です。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 869cffd7abd1aef1dd494b82ae8969bdfd58e68a
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250354"
---
# <a name="view-a-sql-server-audit-log"></a>SQL Server 監査ログの表示
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] を使用して [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で SQL Server 監査ログを表示する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **SQL Server 監査ログを表示する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 **CONTROL SERVER** 権限が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-a-sql-server-audit-log"></a>SQL Server 監査ログを表示するには  
  
1.  オブジェクト エクスプローラーで、 **[セキュリティ]** フォルダーを展開します。  
  
2.  **[監査]** フォルダーを展開します。  
  
3.  表示する監査ログを右クリックし、 **[監査ログの表示]** をクリックします。 **[ログ ファイルの表示 -** _サーバー名\__ ] ダイアログ ボックスが開きます。 詳細については、「 [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md)」を参照してください。  
  
4.  完了したら、 **[閉じる]** をクリックします。  

 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、[ログ ファイルの表示] を使用して監査ログを表示することをお勧めします。 ただし、自動監視システムを作成している場合、[sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) 関数を使用して監査ファイルの情報を直接読み取ることができます。 ファイルを直接読み取ると、わずかに異なる (処理されていない) 形式でデータが返されます。 詳細については、 **sys.fn_get_audit_file** に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Audit &#40;データベース エンジン&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [セキュリティ ログへの SQL Server 監査イベントの書き込み](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  
