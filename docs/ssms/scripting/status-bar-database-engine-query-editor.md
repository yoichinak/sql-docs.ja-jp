---
title: ステータス バー (データベース エンジン クエリ エディター)
description: データベース エンジン クエリ エディター ウィンドウのステータス バーを色分けして、ウィンドウの接続先のデータベース エンジンのインスタンスを示す方法について説明します。
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 228952530dbf3f4d33c86e0154ef84d1ba928cf4
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036249"
---
# <a name="status-bar-database-engine-query-editor"></a>ステータス バー (データベース エンジン クエリ エディター)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウのステータス バーでは、各ウィンドウが [!INCLUDE[ssDE](../../includes/ssde-md.md)] のどのインスタンスに接続しているかを色分けして示すことができます。

1. **作業を開始する準備:** [ステータス バーの色](#StatusBarColors)  

2. **サーバーの状態の色を設定するには:** [オブジェクト エクスプローラー](#SetOEServerColor)、[登録済みサーバー](#SetRegServerColor)  

3. **状態の色を使用するには:** [サーバーの色を使用したクエリ エディターの起動](#OpenServerColor)、[状態の色の指定によるクエリ エディターの起動](#OpenSpecColor)  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

##  <a name="status-bar-colors"></a><a name="StatusBarColors"></a> ステータス バーの色

**[オブジェクト エクスプローラー]** または **[登録済みサーバー]** の特定のサーバー ノードとステータス バーの色を関連付けることができます。 ステータス バーの色を指定できるのは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続されているサーバー ノードのみで、他の SQL Server テクノロジのノードでは指定できません。 また、新しい [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウを [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続するたびに、作成したステータス バーの色を指定することもできます。 その後、サーバー ノードに定義された状態の色を使用してクエリ エディター ウィンドウを開くか、そのエディター ウィンドウに対して一意の色を指定することができます。  

オブジェクト エクスプローラーのサーバー ノードに対して、作成したステータス バーの色を設定する場合、その設定を接続時に行う必要があります。 既存のサーバー ノードに関連付けられている色を変更するには、接続解除してから、新しい色を指定して再接続する必要があります。  

##  <a name="set-the-status-color-for-a-server-in-object-explorer"></a><a name="SetOEServerColor"></a> オブジェクト エクスプローラーでのサーバー状態の色の設定

**オブジェクト エクスプローラーでサーバー状態の色を設定するには**  
  
1.  **[オブジェクト エクスプローラー]** で、 **[接続]** をクリックし、次に **[データベース エンジン...]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログで、 **[オプション >>]** を選択します。  
  
3.  **[作成した色を使用する]** チェック ボックスをオンにします。  
  
4.  色を選択するには、 **[選択...]** をクリックします。  
  
5.  基本の色または作成した色を選択して、[OK] をクリックします。  
  
6.  残りの接続情報を入力して、 **[接続]** ボタンをクリックします。  
  
##  <a name="set-the-status-color-for-a-registered-server"></a><a name="SetRegServerColor"></a> 登録済みサーバーの状態の色の設定  
 **登録済みサーバーの状態の色を設定するには**  
  
1.  **[登録済みサーバー]** で、サーバー ノードを右クリックして、 **[プロパティ...]** をクリックします。  
  
2.  **[サーバー登録プロパティの編集]** ダイアログ ボックスで、 **[接続プロパティ]** タブをクリックします。  
  
3.  **[作成した色を使用する]** チェック ボックスをオンにします。  
  
4.  色を選択するには、 **[選択...]** をクリックします。  
  
5.  基本の色または作成した色を選択して、[OK] をクリックします。  
  
6.  **[サーバー登録プロパティの編集]** ダイアログ ボックスで、 **[保存]** ボタンをクリックします。  
  
##  <a name="open-an-editor-using-a-server-color"></a><a name="OpenServerColor"></a> サーバーの色を使用したエディターの起動  
 **サーバーの色を使用してエディター ウィンドウを開くには**  
  
-   **オブジェクト エクスプローラー** または **[登録済みサーバー]** でサーバー ノードを右クリックして、 **[新しいクエリ]** をクリックします。  
  
-   または、サーバー ノードを強調表示して、 **[新しいクエリ]** ツール バー ボタンをクリックします。  
  
-   エディター ウィンドウのステータス バーでは、関連付けられたサーバーに定義されている色が使用されます。  
  
##  <a name="open-an-editor-specifying-a-status-color"></a><a name="OpenSpecColor"></a> 状態の色の指定によるエディターの起動  
 **状態の色を指定してエディター ウィンドウを開くには**  
  
-   **[ファイル]** メニューの **[新規作成]** をポイントし、 **[データベース エンジン クエリ]** をクリックします。  
  
-   **[サーバーへの接続]** ダイアログで、 **[オプション >>]** を選択します。  
  
-   **[作成した色を使用する]** チェック ボックスをオンにします。  
  
-   色を選択するには、 **[選択...]** をクリックします。  
  
-   基本の色または作成した色を選択して、[OK] をクリックします。  
  
-   残りの接続情報を入力して、 **[接続]** ボタンをクリックします。  
  
## <a name="see-also"></a>参照  
 [クエリおよびテキスト エディター &#40;SQL Server Management Studio&#41;](../f1-help/database-engine-query-editor-sql-server-management-studio.md?view=sql-server-ver15)  
  
