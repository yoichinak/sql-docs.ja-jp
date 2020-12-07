---
description: イベントの転送先サーバーを指定する
title: イベントの転送先サーバーを指定する
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3c30588555fafa4922af3434271759614f19b1df
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037995"
---
# <a name="designate-an-events-forwarding-server"></a>イベントの転送先サーバーを指定する
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server での相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベントの転送先サーバーを指定する方法について説明します。 イベントの転送の適用対象は、単一のコンピューターでホストされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス間で転送されるイベントではなく、サーバー間で転送されるイベントであることに注意してください。 また、転送されたイベントを受信するには、警告管理サーバーが SQL Server の既定のインスタンスでなければならないことにも注意してください。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>はじめに  
  
### <a name="security"></a><a name="Security"></a>セキュリティ  
  
#### <a name="permissions"></a><a name="Permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-designate-an-events-forwarding-server"></a>イベントの転送先サーバーを指定するには  
  
1.  **オブジェクト エクスプ ローラー** で、プラス記号をクリックして、別のサーバーにイベントを転送するサーバーを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** を選択します。  
  
3.  **[SQL Server エージェントのプロパティ - **_<サーバー名>]_ ダイアログ ボックスの **[ページの選択]** で **[詳細設定]** を選択します。  
  
4.  **[SQL Server イベントの転送]** で、 **[イベントを別のサーバーに転送する]** チェック ボックスをオンにします。  
  
5.  **[サーバー]** ボックスの一覧でサーバーを選択し、 **[イベント]** で次のいずれかの操作を行います。  
  
    -   ローカルの警告で処理されていないイベントのみを転送する場合は、 **[未処理のイベント]** をクリックします。  
  
    -   ローカルの警告によって処理されたかどうかにかかわらず、すべてのイベントを転送する場合は、 **[すべてのイベント]** をクリックします。  
  
6.  **[次のレベル以上のイベント発生時]** ボックスの一覧で、選択したサーバーにイベントを転送するときの重大度レベルをクリックします。  
  
7.  完了したら、 **[OK]** をクリックします。  
