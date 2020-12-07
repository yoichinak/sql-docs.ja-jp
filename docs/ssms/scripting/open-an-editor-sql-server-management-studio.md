---
title: エディターの表示 (SQL Server Management Studio)
description: SQL Server Management Studio でデータベース エンジン クエリ、MDX、DMX、および XML/A エディターを開く方法について説明します。
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 5d654a60-d205-49d2-a831-b3d986d60024
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66b83e6c2a26f5fb9f8c2676dc3245d4d79e080e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036485"
---
# <a name="open-an-editor-sql-server-management-studio"></a>エディターの表示 (SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

このトピックでは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター、MDX エディター、DMX エディター、または XML/A エディターを [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で開く方法について説明します。 エディターを開くと、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]の中央のペインに、それぞれのエディター ウィンドウがタブとして表示されます。  
  
## <a name="before-you-begin"></a>はじめに  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] は、4 つのエディターをサポートしています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] スクリプトを編集するための [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディター、これらの言語を使用してスクリプトを編集するための DMX エディターと MDX エディター、そして、XML/A スクリプトまたは XML ファイルを編集するための XML/A エディターです。 テキスト ファイルの編集は、すべてのエディターで行うことができます。  
  
### <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 異なるコード ページを使用する別サイトのユーザーとファイルを共有する場合、ファイル読み込み時のエラーを回避するため、適切な Unicode コード ページでファイルを保存してください。 また、UNIX または Macintosh 用にファイルを保存する場合、適切なドキュメント形式で保存してください。 **[ファイル]** メニューの **[名前を付けて保存]** をクリックし、 **[保存]** ボタンの横にある下矢印をクリックして表示されるメニューの **[エンコード付きで保存]** をクリックします。それから、 **[行の終わり]** ボックスの **[Unix]** または **[Macintosh]** をクリックします。  
  
### <a name="permissions"></a>アクセス許可  
 コード エディター内で実行する操作には、ログインに使用した認証アカウントに付与されている権限が適用されます。 たとえば、Windows 認証を使用して [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウを開いた場合、自分の Windows ログイン アカウントでアクセスできないオブジェクトを参照する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行することはできません。  
  
## <a name="how-to-open-editors"></a>方法:エディターを開く  
 このセクションでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の各種エディターを開く方法について説明します。  
  
### <a name="using-the-filenew-menu"></a>[ファイル] メニューの [新規作成] の使用  
 **[ファイル]** メニューの **[新規作成]** をクリックし、次のいずれかのクエリ エディター オプションを選択します。  
  
-   **[クエリを現在の接続で実行]** : 現在の接続に関連付けられている種類の新しいエディター ウィンドウを [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で開きます。 現在の接続と同じ認証情報がエディター ウィンドウでも使用されます。 たとえば、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスをオブジェクト エクスプローラーで選択してから **[クエリを現在の接続で実行]** を使用した場合、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] に表示される [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターは、同じインスタンスに、同じ認証情報を使用して接続されます。  
  
-   **[データベース エンジン クエリ]** : 新しい [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターが開き、[!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続するために必要な情報を指定するためのダイアログが表示されます。  
  
-   **[Analysis Services MDX クエリ]** : 新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX クエリ エディターが開き、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続するために必要な情報を指定するためのダイアログが表示されます。  
  
-   **[Analysis Services DMX クエリ]** : 新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DMX クエリ エディターが開き、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続するために必要な情報を指定するためのダイアログが表示されます。  
  
-   **[Analysis Services XML/A クエリ]** : 新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XML/A クエリ エディターが開き、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続するために必要な情報を指定するためのダイアログが表示されます。  
  
### <a name="using-the-fileopen-menu"></a>[ファイル] メニューの [開く] の使用  
 **[ファイル]** メニューの **[開く]** をクリックし、目的のファイルに移動して開きます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] にはファイル拡張子に対応する適切な種類のエディターが表示されます。さらに、ファイルの内容がエディター ウィンドウにコピーされ、必要に応じて接続ダイアログが表示されます。 たとえば、.sql という拡張子のファイルを開いた場合、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] に [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが開き、.sql ファイルの内容がコピーされて、接続ダイアログが表示されます。 開こうとするファイルの拡張子が特定のエディターに関連付けられていない場合、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のテキスト エディター ウィンドウが開いて、ファイルの内容がコピーされます。  
  
 詳細については、「 [ファイル拡張子をコード エディターに関連付ける方法](./associate-file-extensions-to-a-code-editor.md)」を参照してください。  
  
### <a name="using-the-toolbar"></a>ツール バーの使用  
 **[標準]** ツール バーで、次のいずれかのボタンをクリックします。  
  
-   **[新しいクエリ]** : 現在の接続に関連付けられている種類の新しいエディター ウィンドウを [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で開きます。 現在の接続と同じ認証情報がエディター ウィンドウでも使用されます。 たとえば、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスをオブジェクト エクスプローラーで選択してから **[新しいクエリ]** ボタンをクリックした場合、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] に表示される [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターは、同じインスタンスに、同じ認証情報を使用して接続されます。  
  
-   **[データベース エンジン クエリ]** : 新しい [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターが開き、[!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続するために必要な情報を指定するためのダイアログが表示されます。  
  
-   **[Analysis Services MDX クエリ]** : 新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX クエリ エディターが開き、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続するために必要な情報を指定するためのダイアログが表示されます。  
  
-   **[Analysis Services DMX クエリ]** : 新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DMX クエリ エディターが開き、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続するために必要な情報を指定するためのダイアログが表示されます。  
  
-   **[Analysis Services XML/A クエリ]** : 新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XML/A クエリ エディターが開き、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続するために必要な情報を指定するためのダイアログが表示されます。  
  
### <a name="using-object-explorer"></a>オブジェクト エクスプローラーの使用  
 **オブジェクト エクスプローラー**から次の操作を行います。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続されたサーバー ノードを右クリックし、 **[新しいクエリ]** を選択します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の同じインスタンスに接続された [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが開いて、このウィンドウのデータベース コンテキストが、ログインの既定のデータベースに設定されます。  
  
-   データベース ノードを右クリックし、 **[新しいクエリ]** を選択します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の同じインスタンスに接続された [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが開いて、このウィンドウのデータベース コンテキストが、同じデータベースに設定されます。  
  
### <a name="using-solution-explorer"></a>ソリューション エクスプローラーの使用  
 **ソリューション エクスプローラー**で、フォルダーを展開してフォルダー内の項目を右クリックし、 **[開く]** をクリックするか、項目またはファイルをダブルクリックします。  
  
### <a name="using-template-browser-to-open-the-database-engine-query-editor"></a>テンプレート ブラウザーを使用してデータベース エンジン クエリ エディターを開く方法  
  
-   **[表示]** メニューの **[テンプレート エクスプローラー]** をクリックします。  
  
-   右ペインに **[テンプレート ブラウザー]** ウィンドウが表示されます。  
  
-   テンプレートをダブルクリックして、データベース エンジン クエリ ウィンドウを開きます。このウィンドウには、テンプレートのテキストが表示されます。 たとえば、CREATE DATABASE テンプレートを開くには、 **[SQL Server テンプレート]** フォルダー、 **[Database]** フォルダーの順に開き、 **[create database]** をダブルクリックします。