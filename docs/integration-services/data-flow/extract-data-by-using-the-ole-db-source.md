---
description: OLE DB ソースを使用してデータを抽出する
title: OLE DB ソースを使用してデータを抽出する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: 4ca6eeb5-b60e-4b81-86dd-0674be8ae8d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 15e55ec942331ef14458aad461c5b7c9432b0d6e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430844"
---
# <a name="extract-data-by-using-the-ole-db-source"></a>OLE DB ソースを使用してデータを抽出する

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  OLE DB ソースを追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクがあらかじめ含まれている必要があります。  
  
### <a name="to-extract-data-using-an-ole-db-source"></a>OLE DB ソースを使用してデータを抽出するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、OLE DB ソースをデザイン画面にドラッグします。  
  
4.  OLE DB ソースをダブルクリックします。  
  
5.  **[OLE DB ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで、既存の OLE DB 接続マネージャーを選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。 詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
6.  データのアクセス方法を、次の中から選択します。  
  
    -   **[テーブルまたはビュー]** OLE DB 接続マネージャーの接続先となる、データベースのテーブルまたはビューを選択します。  
  
    -   **[テーブル名またはビュー名の変数]** OLE DB 接続マネージャーの接続先となるデータベースのテーブルまたはビューの名前が含まれる、ユーザー定義変数を選択します。  
  
    -   **[SQL コマンド]** SQL コマンドを入力するか、 **[クエリ ビルダー]** で **[クエリの作成]** をクリックして、SQL コマンドを記述します。  
  
        > [!NOTE]  
        >  コマンドにはパラメーターを含めることができます。 詳細については、「 [クエリ パラメーターをデータ フロー コンポーネントの変数にマップする](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)」を参照してください。  
  
    -   **[変数からの SQL コマンド]** SQL コマンドが含まれるユーザー定義変数を選択します。  
  
        > [!NOTE]  
        >  変数は、OLE DB ソースを含む同じデータ フロー タスクのスコープ内、または同じパッケージのスコープ内で定義する必要があります。また、変数は文字列データ型である必要があります。  
  
7.  外部列と出力列間のマッピングを更新するには、 **[列]** をクリックし、 **[外部列]** 一覧にある別の列を選択します。  
  
8.  必要に応じて、 **[出力列]** 一覧の値を編集し、出力列の名前を更新します。  
  
9. エラー出力を構成するには、 **[エラー出力]** をクリックします。 詳細については、「 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md)」を参照してください。  
  
10. **[プレビュー]** をクリックすると、OLE DB ソースによって抽出されたデータを最大 200 行表示できます。  
  
11. **[OK]** をクリックします。  
  
12. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [OLE DB ソース](../../integration-services/data-flow/ole-db-source.md)   
 [Integration Services の変換](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../integration-services/data-flow/integration-services-paths.md)   
 [データ フロー タスク](../../integration-services/control-flow/data-flow-task.md)  
  
  
