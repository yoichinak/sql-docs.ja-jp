---
description: コレクション セットの開始または停止
title: コレクション セットの開始または停止 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- collection sets [SQL Server], stopping
- collection sets [SQL Server], starting
ms.assetid: 48a7b2fe-6bc3-4278-a7ec-1babc1290345
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1d62c72e43d9495874881ba3c029640626f129c8
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88471451"
---
# <a name="start-or-stop-a-collection-set"></a>コレクション セットの開始または停止
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でコレクション セットを開始または停止する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
     [Security](#Security)  
  
-   **コレクション セットを開始または停止する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   データ コレクターのストアド プロシージャとカタログ ビューは、 **msdb** データベースに格納されます。  
  
-   通常のストアド プロシージャとは異なり、データ コレクターで使用するストアド プロシージャではパラメーターのデータ型が厳密に定義されており、データ型の自動変換はサポートされていません。 これらのパラメーターが、引数の説明で指定されている正しいデータ型で呼び出されないと、このストアド プロシージャではエラーが返されます。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
  
-   SQL Server エージェントが開始されている必要があります。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
  
-   コレクション セットに関する情報を取得するには、 [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) カタログ ビューのクエリを実行します。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 **dc_operator** 固定データベース ロールのメンバーシップが必要です。 コレクション セットにプロキシ アカウントがない場合は、 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-start-a-collection-set"></a>コレクション セットを開始するには  
  
1.  オブジェクト エクスプローラーで、 **[管理]** ノード、 **[データ コレクション]** 、 **[システム データ コレクション セット]** の順に展開します。  
  
2.  開始するコレクション セットを右クリックして **[データ コレクション セットの開始]** をクリックします。  

     メッセージ ボックスにはこのアクションの結果が表示され、コレクション セットのアイコンに緑色の矢印が付いている場合は、コレクション セットが開始されていることを示します。  
  
#### <a name="to-stop-a-collection-set"></a>コレクション セットを停止するには  
  
1.  オブジェクト エクスプローラーで、 **[管理]** ノード、 **[データ コレクション]** 、 **[システム データ コレクション セット]** の順に展開します。  
  
2.  停止するコレクション セットを右クリックして **[データ コレクション セットの停止]** をクリックします。  
  
     メッセージ ボックスにはこのアクションの結果が表示され、コレクション セットのアイコンに赤い丸が付いている場合は、コレクション セットが停止していることを示します。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-start-a-collection-set"></a>コレクション セットを開始するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_syscollector_start_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md) を使用して、ID が `1`であるコレクション セットを開始します。  
  
```sql  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
#### <a name="to-stop-a-collection-set"></a>コレクション セットを停止するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md) を使用して、ID が `1`であるコレクション セットを停止します。  
  
```sql  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>参照  
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
