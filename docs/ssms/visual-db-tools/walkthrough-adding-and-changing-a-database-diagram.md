---
description: チュートリアル:データベース ダイアグラムの追加と変更
title: データベース ダイアグラムの追加と変更
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- database diagrams [SQL Server], about database diagrams
- database diagrams [SQL Server], designing
- database diagrams [SQL Server], creating
ms.assetid: 228caa0d-8f24-46ab-86d1-b6d8631322bc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 87ff469370e58c261e762cf9c4d6c604488ccfb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479925"
---
# <a name="walkthrough-adding-and-changing-a-database-diagram"></a>チュートリアル:データベース ダイアグラムの追加と変更
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
このチュートリアルでは、データベース ダイアグラムを作成および変更する方法と、データベース ダイアグラム コンポーネントを使用してデータベースを変更する方法について説明します。 ダイアグラムにテーブルを追加する方法、テーブル間のリレーションシップを作成する方法、列に制約とインデックスを作成する方法、およびテーブルごとに表示する情報のレベルを変更する方法を記載しています。  
  
## <a name="prerequisites"></a>必須コンポーネント  
このチュートリアルを完了するための要件は次のとおりです。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースへのアクセス権  
  
-   データベース所有者 **dbo** 特権のあるアカウント  
  
> [!NOTE]  
> 十分な特権がないアカウントを使用してテーブルを変更しようとすると、エラー メッセージが表示されます。  
  
## <a name="creating-a-diagram"></a>ダイアグラムの作成  
  
#### <a name="to-create-a-new-database-diagram"></a>新しいデータベース ダイアグラムを作成するには  
  
1.  **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
2.  [データベース] ノードを展開し、[ [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ] ノードを展開します。  
  
3.  [データベース ダイアグラム] ノードを右クリックし、**[新しいデータベース ダイアグラム]** をクリックします。  
  
    ダイアグラムの作成に必要なオブジェクトがデータベースに含まれていない場合、" **このデータベースには、データベース ダイアグラムの作成を使用するために必要な 1 つ以上のサポート オブジェクトが含まれていません。サポート オブジェクトを作成しますか?**" というメッセージが表示されます。 **[はい]** をクリックします。  
  
    **[テーブルの追加]** ダイアログ ボックスが表示されます。  
  
4.  **[AddressType (Person)]** と **[Address (Person)]** を選択し、 **[追加]** をクリックします。  
  
    2 つのテーブルがダイアグラムに追加されます。  
  
5.  **[テーブルの追加]** ダイアログ ボックスを閉じます。  
  
#### <a name="to-view-different-column-data"></a>異なる列データを表示するには  
  
1.  `Address` テーブルを右クリックします。 ショートカット メニューの **[テーブル ビュー]** をポイントし、 **[標準]** をクリックします。  
  
    テーブル グリッドに **[列名]**、 **[データ型]**、および **[Null を許容]** という 3 つの列が表示されます。  
  
2.  `Address` テーブルを右クリックし、 **[テーブル ビュー]** をクリックして、 **[キー]** を選択します。  
  
    テーブル グリッドに、テーブルの列名が列挙された 1 つの列が表示されます。 表示されるのは、インデックスとして使用されている列のみです。  
  
## <a name="creating-new-tables"></a>新しいテーブルの作成  
  
#### <a name="to-create-tables-within-diagram-designer"></a>ダイアグラム デザイナー内でテーブルを作成するには  
  
1.  ダイアグラム デザイナーで、既存のテーブル以外の場所を右クリックし、 **[新しいテーブル]** をクリックします。  
  
2.  **[名前の選択]** ダイアログ ボックスで、 **[OK]** をクリックして既定の名前の **Table1**をそのまま使用します。  
  
    新しいテーブル グリッドに **[列名]**、 **[データ型]**、および **[Null を許容]** という 3 つの列が表示されます。  
  
3.  **Table1**に次のデータを追加します。  
  
    |**列名**|**[データ型]**|**[NULL を許容]**|  
    |-------------------|-----------------|-------------------|  
    |**T1col1**|**int**|checked|  
    |**T1col2**|**varchar (50)**|checked|  
    |**T1col3**|**float**|checked|  
  
4.  [ `T1col1` ] を右クリックし、 **[主キーの設定]** をクリックします。  
  
    列名の隣に鍵のアイコンが表示されます。  
  
5.  **[ファイル]** メニューの **[Diagram1 を保存]** をクリックします。  
  
6.  **[名前の選択]** ダイアログ ボックスで、 **[OK]** をクリックして既定の名前の **Diagram1**をそのまま使用します。  
  
7.  **[上書き保存]** ダイアログ ボックスに、 `Table1` がデータベースに保存されることを示すメッセージが表示されます。 **[はい]** をクリックします。  
  
## <a name="modifying-table-structure"></a>テーブル構造の変更  
ダイアグラム デザイナーで CHECK 制約を追加し、テーブル間のリレーションシップを作成できます。  
  
#### <a name="to-create-check-constraints"></a>CHECK 制約を作成するには  
  
1.  `Table1`で、[ `T1col3` ] 行を右クリックし、 **[CHECK 制約]** をクリックします。  
  
    **[CHECK 制約]** ダイアログ ボックスが表示されます。  
  
2.  **[追加]** をクリックします。  
  
    **[制約された制約のチェック]** の一覧に、既定の `CK_Table1`という名前を持つ新しい制約が表示されます。  
  
3.  グリッド内の **[式]** 行をクリックし、参照ボタンをクリックします。  
  
    **[選択された制約のチェック]** ダイアログ ボックスが表示されます。  
  
4.  「**T1col3 > 5**」と入力して **[OK]** をクリックします。  
  
    `Table1` これで `T1col3` に入力されるすべての値が 5 よりも大きくなければならないという制約が追加されます。  
  
5.  **[閉じる]** をクリックします。  
  
#### <a name="to-create-relationships-between-tables"></a>テーブル間のリレーションシップを作成するには  
  
1.  ダイアグラム デザイナーで、 `Table2` という新しいテーブルを作成し、次の列を追加します。  
  
    |**列名**|**[データ型]**|**[NULL を許容]**|  
    |-------------------|-----------------|-------------------|  
    |**T2col1**|**int**|オフ|  
    |**T2col2**|**varchar (50)**|checked|  
    |**T2col3**|**xml**|checked|  
  
    > [!NOTE]  
    > 外部キー リレーションシップの主キー側の列は、主キーまたは UNIQUE 制約に含まれている必要があります。  
  
2.  `T2col1` を `T1col1`にドラッグします。  
  
    **[外部キーのリレーションシップ]** ダイアログ ボックスと **[テーブルと列]** ダイアログ ボックスが表示されます。[テーブルと列] ダイアログ ボックスが手前に表示されます。  
  
3.  **[OK]** をクリックして、新しいリレーションシップを保存します。  
  
4.  もう一度 **[OK]** をクリックします。  
  
## <a name="creating-indexes"></a>インデックスの作成  
XML を含めて、ほとんどの種類のデータにインデックスを作成できます。  
  
#### <a name="to-create-a-standard-index"></a>標準のインデックスを作成するには  
  
1.  `Table1` を右クリックし、 **[インデックス/キー]** をクリックします。  
  
    **[インデックス/キー]** ダイアログ ボックスが表示されます。  
  
2.  **[追加]** をクリックします。  
  
    **[選択された主/一意キーまたはインデックス]** の一覧に、既定の `IX_Table1`という名前を持つ新しいインデックスが表示されます。  
  
3.  **[列]** 行を選択し、参照ボタンをクリックします。  
  
    **[インデックスの列]** ダイアログ ボックスが表示されます。  
  
4.  **[列名]** の下にあるドロップダウン リストの下矢印をクリックして、[ `T1col2`] をクリックします。  
  
    > [!NOTE]  
    > `T1col2` の下にあるセルを選択し、別の列名を選択することにより、このインデックスに列を追加できます。  
  
5.  **[OK]** をクリックしてこのインデックスを保存します。  
  
6.  **[インデックス/キー]** ダイアログ ボックスで **[閉じる]** をクリックします。  
  
#### <a name="to-create-an-xml-index"></a>XML インデックスを作成するには  
  
1.  [ `T2col1` ] を右クリックし、 **[主キーの設定]** を選択します。  
  
    > [!NOTE]  
    > XML インデックスを追加するには、テーブル内にある別の列がクラスター化主キーに設定されている必要があります。  
  
2.  `T2col3` の [ `Table2` ] 行を右クリックし、 **[XML インデックス]** をクリックします。  
  
    **[XML インデックス]** ダイアログ ボックスが表示されます。  
  
3.  **[追加]** をクリックします。  
  
    XML インデックスが **[選択された XML インデックス]** の一覧に既定の名前で追加されます。  
  
4.  **[閉じる]** をクリックします。  
  
    > [!NOTE]  
    > XML インデックスは列単位に作成されます。 最初の XML インデックスがプライマリ インデックス、その他のインデックスがセカンダリ インデックスになります。  
  
## <a name="saving-the-diagram"></a>ダイアグラムの保存  
ダイアグラムに加えた変更は、そのダイアグラムを保存するまでデータベースに送信されません。 問題や競合が発生した場合、ダイアログ ボックスにその詳細が表示されます。  
  
#### <a name="to-save-a-database-diagram"></a>データベース ダイアグラムを保存するには  
  
1.  **[ファイル]** メニューの **[Diagram1 の保存]** を選択します。  
  
    **[上書き保存]** ダイアログ ボックスが表示されます。 **[該当テーブルに関する警告]** チェック ボックスがオンになっている場合、新しいテーブルや変更されるテーブルの一覧が表示されます。  
  
2.  **[OK]** をクリックします。  
  
3.  エラーが発生した場合は、 **[保存前の通知]** ダイアログ ボックスにそれらのエラーと原因が表示されます。 エラーを修正し、再度ダイアグラムを保存します。  
  
## <a name="next-steps"></a>次の手順  
ここで作成したダイアグラムは、既存のテーブルと新しいテーブルを 2 つずつ使用しただけの基本的なものですが、既存のデータベースのダイアグラムを作成したり、視覚的に新しいスキーマを作成したりできることを示しています。 さらに理解を深めるには、次の操作を行うことをお勧めします。  
  
-   関連テーブルのグループを含む新しいダイアグラムの作成  
  
-   テーブルごとに表示される情報量のカスタマイズ  
  
-   レイアウトの変更と注釈の追加  
  
-   ビットマップへのダイアグラムのコピー  
  
## <a name="see-also"></a>参照  
[ダイアグラムに表示される情報の量のカスタマイズ (Visual Database Tools)](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)  
[データベース ダイアグラム デザイナーの設定 (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
[ダイアグラムへのテーブルの追加 (Visual Database Tools)](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
[ダイアグラムでテーブル間のリレーションシップを作成する方法 (Visual Database Tools)](../../ssms/visual-db-tools/create-relationships-between-tables-on-a-diagram-visual-database-tools.md)  
[XML インデックスの作成](../../relational-databases/xml/create-xml-indexes.md)  
[クリップボードへのデータベース ダイアグラムのイメージのコピー (Visual Database Tools)](../../ssms/visual-db-tools/copy-an-image-of-a-database-diagram-to-the-clipboard-visual-database-tools.md)  
[ダイアグラムのレイアウトの操作 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  
