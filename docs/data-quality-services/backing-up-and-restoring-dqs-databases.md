---
description: DQS データベースのバックアップと復元
title: DQS データベースのバックアップと復元
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3091f62-2234-4a80-a615-cf14c2a1da85
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 03b58daec9def4e902e111719353110bfad1d69b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450005"
---
# <a name="backing-up-and-restoring-dqs-databases"></a>DQS データベースのバックアップと復元

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、DQS データベースのバックアップと復元を行う方法について説明します。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
  
-   DQS サーバーのインストール中に入力したデータベース マスター キーのパスワードを知っている必要があります。  
  
-   DQS で実行中のアクティビティまたはプロセスがないことを確認します。 これは **[アクティビティ監視]** 画面を使用して確認できます。 この画面の操作の詳細については、「 [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md)」を参照してください。  
  
-   DQS サーバーにログオンしているユーザーがないことを確認します。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
  
-   バックアップおよび復元操作を実行するには、使用する Windows ユーザー アカウントが、SQL Server インスタンスの sysadmin 固定サーバー ロールのメンバーであることが必要です。  
  
-   DQS の実行中のアクティビティを終了させたり実行中のプロセスを停止させたりするには、DQS_MAIN データベースの dqs_administrator ロールが必要です。  
  
##  <a name="backup-and-restore-dqs-databases"></a><a name="BackupRestore"></a> DQS データベースのバックアップと復元  
  
1.  Microsoft SQL Server Management Studio を起動し、適切な SQL Server インスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで、 **[データベース]** ノードを展開します。  
  
3.  DQS_STAGING_DATA データベースをバックアップします。 SQL Server データベースのバックアップ手順について詳しくは、「[データベースの完全バックアップの作成 &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)」をご覧ください。  
  
4.  DQS_PROJECTS データベースをバックアップします。  
  
5.  DQS_MAIN データベースをバックアップします。  
  
6.  SQL Server の現在のインスタンスから切断し、データベースを復元する SQL Server インスタンスに接続します。  
  
7.  DQS_MAIN データベースを復元します。 SQL Server データベースを復元する手順については、「[SSMS を使用したデータベース バックアップの復元](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)」をご覧ください。  
  
8.  DQS_PROJECTS データベースを復元します。  
  
9. DQS_STAGING_DATA データベースを復元します。  
  
10. オブジェクト エクスプローラーでサーバーを右クリックし、 **[新しいクエリ]** をクリックします。  
  
11. クエリエディターウィンドウで、次の SQL ステートメントをコピーし、を *\<PASSWORD>* DQS のインストール時にデータベースマスターキーに対して指定したパスワードに置き換えます。  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    EXECUTE [internal_core].[RestoreDQDatabases] '<PASSWORD>'  
    GO  
  
    ```  
  
12. F5 キーを押してステートメントを実行します。 **[結果]** ペインを確認してステートメントが正常に実行されたことを確認します。  
  
## <a name="see-also"></a>参照  
 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)  
  
  
