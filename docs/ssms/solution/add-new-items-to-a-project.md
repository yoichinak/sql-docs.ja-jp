---
description: プロジェクトへの新規項目の追加
title: プロジェクトへの新規項目の追加
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 76af8692-324f-4f5e-b1a0-d72ca8a107e3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7b3b36bfa75c39a4acc0c41c8dae5199b7973391
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036055"
---
# <a name="add-new-items-to-a-project"></a>プロジェクトへの新規項目の追加
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
プロジェクトに新しい項目を追加して、アプリケーションの機能を拡張できます。 新しい項目にできるのは、クエリまたは接続です。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプト プロジェクトおよび Analysis Services スクリプト プロジェクトという 2 種類のプロジェクトがあります。 プロジェクトの種類によって、プロジェクトに追加できるアイテムが決まります。 たとえば、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ (拡張子が .sql のファイル) は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプト プロジェクトには追加できますが、Analysis Services スクリプト プロジェクトには追加できません。  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、プロジェクト内にフォルダーを作成することはできません。 作業を整理するには、ソリューション内に複数のプロジェクトを作成してください。  
  
### <a name="to-add-a-new-query-to-an-existing-project"></a>既存のプロジェクトに新しいクエリを追加するには  
  
1.  ソリューション エクスプローラーで、対象のプロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。  
  
3.  **[新しい項目の追加]** ダイアログ ボックスの左側のペインで、カテゴリを選択します。  
  
4.  右側のペインでクエリ テンプレートを選択し、 **[追加]** をクリックします。 新しいクエリがプロジェクトの **[クエリ]** フォルダーに追加されます。  
  
5.  **[データベース エンジンへの接続]** ダイアログ ボックスで、新しいクエリの接続を指定し、 **[接続]** をクリックします。 新しいクエリに接続を関連付けたくない場合は、接続ダイアログの **[キャンセル]** をクリックすることもできます。  
  
6.  必要に応じて、ソリューション エクスプローラーでクエリの名前を変更します。  
  
### <a name="to-add-a-new-connection-to-an-existing-project"></a>既存のプロジェクトに新しい接続を追加するには  
  
1.  ソリューション エクスプローラーで、対象のプロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。  
  
3.  左ペインで **[接続]** を選択します。  
  
4.  右側のペインで **[新しい接続]** を選択し、 **[追加]** をクリックします。  
  
5.  **[データベース エンジンへの接続]** ダイアログ ボックスで、新しいクエリの接続を指定し、 **[接続]** をクリックします。 新しい接続がプロジェクトの **[接続]** フォルダーに追加されます。  
  
## <a name="see-also"></a>参照  
[ソリューション エクスプローラー](../../ssms/solution/solution-explorer.md)  
[ファイル拡張子をコード エディターに関連付ける](../scripting/associate-file-extensions-to-a-code-editor.md)  
[既存の項目をプロジェクトに追加する](../../ssms/solution/add-existing-items-to-a-project.md)  
[アイテムやプロジェクトのクリアまたは削除](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
