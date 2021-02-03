---
title: 統計の変更 | Microsoft Docs
description: SQL Server Management Studio または Transact-SQL を使用し、SQL Server の既存の統計値を変更する方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fa0aaa1bc1f011814c44ae881dd6d24dc66e7698
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250274"
---
# <a name="modify-statistics"></a>統計の変更
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して既存の統計を変更できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **統計を変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 以下の条件が必要です:  
  
-   ユーザーは、テーブルまたはビューに対する ALTER 権限が必要です。  
  
-   ユーザーがテーブルまたはインデックス付きビューの所有者であるか、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、または **db_ddladmin** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-statistics"></a>統計を変更するには  
  
1.  **オブジェクト エクスプローラー** で、統計を変更するデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、統計を変更するテーブルを展開します。  
  
4.  プラス記号をクリックして **[統計]** フォルダーを展開します。  
  
5.  変更する統計オブジェクトを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[統計のプロパティ -**  *statistics_name*] ダイアログ ボックスの **[全般]** ページで **[追加]** 、 **[削除]** 、 **[上へ移動]** 、 **[下へ移動]** 、またはそれらを組み合わせて使い、統計のプロパティを変更します。 **[統計の列]** グリッド内の列の位置は、統計の使いやすさに影響する可能性があることに注意してください。  
  
7.  **[OK]** をクリックします。  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 **統計を変更するには**  
  
 Transact-SQL ステートメントを使用して、このタスクを実行することはできません。 Transact-SQL を使用して統計を変更するには、既存の統計を削除してから新しい属性を再作成します。  
  
 詳細については、「[DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)」および「[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)」を参照してください。  
  
  
