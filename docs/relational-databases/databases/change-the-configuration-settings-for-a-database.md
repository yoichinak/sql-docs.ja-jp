---
title: データベースの構成設定の変更 | Microsoft Docs
description: SQL Server Management Studio または Transact-SQL を使用して、SQL Server 2019 でデータベース レベルのオプションを変更する方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- database configuration [SQL Server]
- configuration options [SQL Server], databases
- modifying database configuration settings
ms.assetid: c29c3385-5043-400f-bb4e-044a4c9a9a4b
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d3e1e312a539ccd3526e252facd523980d751e4b
ms.sourcegitcommit: 00be343d0f53fe095a01ea2b9c1ace93cdcae724
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98813603"
---
# <a name="change-the-configuration-settings-for-a-database"></a>データベースの構成設定の変更
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  このトピックでは、 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベース レベルのオプションを変更する方法について説明します。 データベース オプションは各データベースに一意であり、他のデータベースには影響しません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してデータベースのオプション設定を変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   これらのオプションを変更できるのは、システム管理者、データベース所有者、または **sysadmin** 固定サーバー ロールおよび **dbcreator** 固定サーバー ロールと **db_owner** 固定データベース ロールのメンバーだけです。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>データベースのオプション設定を変更するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、サーバーを展開して **[データベース]** を展開します。データベースを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[データベースのプロパティ]** ダイアログ ボックスで、 **[オプション]** をクリックします。ほとんどの構成設定にアクセスできます。 ファイルとファイル グループの構成、ミラーリングとログ配布の設定については、それぞれ専用のページにあります。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>データベースのオプション設定を変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースに対して、復旧モデルおよびデータ ページ検証のオプションを設定します。  
  
 [!code-sql[DatabaseDDL#AlterDatabase7](../../relational-databases/databases/codesnippet/tsql/change-the-configuration_1.sql)]  
  
 詳細については、「[ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [ALTER DATABASE データベース ミラーリング &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [データベースの名前変更](../../relational-databases/databases/rename-a-database.md)   
 [データベースの圧縮](../../relational-databases/databases/shrink-a-database.md)  
  
  
