---
title: エディターの構成 (SQL Server Management Studio)
description: '[オプション] ダイアログでオプションを設定して。SQL Server Management Studio エディターの操作をカスタマイズする方法について説明します。'
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: e7c7a8ef-f561-4258-a7b6-c445dba69f87
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7da0e6a9eff582e69fa37ccd4396039fe6ac1727
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039096"
---
# <a name="configure-editors-sql-server-management-studio"></a>エディターの構成 (SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] エディターのオプションを構成することにより、各エディターの操作をカスタマイズできます。  
  
## <a name="setting-editor-options"></a>エディター オプションの設定  
 ほとんどのエディター オプションは、 **[ツール]** メニューで **[オプション]** を選択し、 **[オプション]** ダイアログを表示して設定します。 **[オプション]** ダイアログの左ペインの **[テキスト エディター]** ノードを開いて、コードとテキストの編集オプションを設定します。 [テキスト エディター] の下のノードは特定のエディターに適用されます。  
  
1.  **すべての言語**: このノードを使用して設定されたオプションは、すべての [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] エディターに適用されます。 これらの設定は、他のノードを使用して特定のエディターの別のオプションを設定することによりオーバーライドできます。  
  
2.  **プレーンテキスト**: このノードを使用して設定されたオプションは、MDX エディター、DMX エディター、およびテキスト エディターに適用されます。  
  
3.  **Transact-SQL**: このノードを使用して設定されたオプションは、データベース エンジン クエリ エディターに適用されます。  
  
4.  **XML**: このノードを使用して設定されたオプションは、XML for Analysis エディターに適用されます。  
  
 **[クエリ実行]** または **[クエリ結果]** ノードを開いて、クエリの実行やクエリ結果の表示方法をカスタマイズします。  
  
## <a name="editor-configuration-tasks"></a>エディターの構成タスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|エクスプローラーで、指定された拡張子を持つファイルをダブルクリックしたときに開かれるエディターを指定する方法について説明します。|[ファイル拡張子をコード エディターに関連付ける方法](./associate-file-extensions-to-a-code-editor.md)|  
|コードおよびテキストを読みやすくするためにフォントをカスタマイズする方法について説明します。|[フォントの色、サイズ、スタイルを変更する方法](./change-font-color-size-and-style.md)|  
|プロパティの表示方法について説明します。|[Management Studio の [プロパティ] ウィンドウの使用](./use-the-properties-window-in-management-studio.md)|  
|エディター オプション ダイアログの F1 ヘルプ ページの場所です。|[[クエリ オプション] ページの F1 ヘルプ](../f1-help/f1-help-for-server-connections-sql-server-management-studio.md)|