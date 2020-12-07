---
title: Reporting Services で KPI を使用する | Microsoft Docs
description: SQL Server Reporting Services で KPI を使用して、状態とパフォーマンスを簡単に測定する方法について説明します。
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.date: 07/02/2017
ms.openlocfilehash: e661fee4e9b5afe5f78cae444ff8d6574a536bb9
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243781"
---
# <a name="working-with-kpis-in-reporting-services"></a>Reporting Services で KPI を使用する

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

" *主要業績評価指標 (KPI)* " は、目標に対する達成度の伝達を視覚化したものです。  主要業績評価指標は、チーム、マネージャー、およびビジネスにとって、測定可能な目標に対する進捗度をすばやく評価するうえで重要です。
  
SQL Server Reporting Services で KPI を使用することで、以下の質問に対する回答を簡単に視覚化できます。  
  
- どの目標を達成していて、どの目標を達成していないか。  
  
- どの程度進んでいるか、または遅れているか。  
  
- 少なくともどの程度の量を完了したか。  

> [!NOTE]
> KPI にアクセスできるのは、SSRS ポータルの Enterprise (Developer) エディションのみです。

## <a name="creating-a-dataset"></a>データセットの作成

KPI は、共有データセットの最初の行のデータのみを使用します。 使用したいデータがその最初の行にあることを確認します。 共有データセットを作成するには、レポート ビルダーまたは SQL Server Data Tools のいずれかを使用することができます。  
  
> **注** :データセットは、KPI と同じフォルダーに配置する必要はありません。  
  
## <a name="placement-of-kpis"></a>KPI の配置  
  
KPI は、レポート サーバーの任意のフォルダーに作成できます。  KPI を作成する前に、それを配置する適切な場所について検討する必要があります。 他のレポートおよびそれに関する KPI に関係があり、ユーザーが参照できるフォルダーに配置することができます。  
## <a name="adding-a-kpi"></a>KPI を追加する
  
KPI の場所を決定したら、そのフォルダーに移動して、トップ メニューから [ **新規** > **KPI** ] を選択します。  
  
![[新規] ドロップダウン リストを示すスクリーンショット。[KPI] オプションが選択されています。](../reporting-services/media/rscreatekpi1.png)  
  
これにより、 **[新しい KPI]** 画面が表示されます。  
  
![[新しい KPI] 画面を示すスクリーンショット。](../reporting-services/media/rscreatekpi2.png)  
  
静的な値を割り当てるか、共有データセットのデータを使用できます。 新しい KPI を作成する場合、ランダムなデータセットを手動で入力します。  
  
| フィールド | 説明 |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 値の書式 | 表示される値の形式を変更するために使用します。 |
| 値 | 表示する KPI の値。 |
| 目標 | 数値との比較として使用され、比率の差として表示されます。 |
| Status | KPI タイルの色を決定するために使用される数値。 有効な値は 1 (緑)、0 (黄色) および-1 (赤です)。 |
| トレンド セット | グラフを視覚化するために使用されるコンマ区切りの数値。 これは、傾向を表す値を含むデータセットの列にも設定できます。 |
| 関連コンテンツ | ドリルスルー リンクを設定する機能。 このリンクに使用できるのは、ポータルまたはカスタム URL のいずれかで公開されているモバイル レポートです。 |
  
> **警告** : 設計時には [ **ステータス** ] フィールドに文字値を使用できますが、データセットを更新する場合、数値を使用する必要があります。 数値ではなく文字値を含むデータセットを更新すると、サーバー上の KPI が破損する可能性があります。  
>
> **注** : **[値]** 、 **[目標]** 、 **[状態]** の各フィールドの値には、データセットの結果の最初の行からのみ選択できます。 ただし、 **[トレンド セット]** フィールドでは、傾向を反映する列を選択できます。  
  
共有データセットのデータを使用するには、次の手順を実行します。
  
1. フィールド ドロップダウン ボックスを  **手動設定** または **未設定** から **データセット フィールド** に変更します。  
  
    ![[値] オプションが [データセット フィールド] に設定され、[データセット フィールドの選択] が [未設定] に設定されていることを示すスクリーンショット。](../reporting-services/media/rscreatekpi3.png)  
  
2. データ ボックスで **省略記号 [...]** を選択します。 これにより、 **[データセットの選択]** 画面が表示されます。  
  
    ![[データセットの選択] セクションのスクリーンショット。[Finance_KPI] オプションが選択されています。](../reporting-services/media/rscreatekpi4.png)  
  
3. 表示するデータを含むデータセットを選択します。  
  
4. 使用するフィールドを選択します。 **[OK]** を選択します。  
  
    ![[Finance_KPI] セクションの [フィールドの選択] を示すスクリーンショット。[Sum_Amount] オプションが選択されています。](../reporting-services/media/rscreatekpi5.png)  
  
5. 値の形式と一致するように **[値の表示形式]** を変更します。 この例では、値は通貨です。  
  
    ![[値の表示形式] オプションが [通貨] に設定されていることを示している KPI プレビューのスクリーンショット。](../reporting-services/media/rscreatekpi6.png)  
  
6. **[適用]** を選択します。  
  
    ![データセットに 2 つの項目があることを示している KPI のスクリーンショット。](../reporting-services/media/rscreatekpi7.png)

## <a name="configuring-related-content"></a>関連するコンテンツの構成

**モバイル レポート** を選択したときは、ダイアログでリンク先を選択できます。

   ![[関連するコンテンツ] オプションが [モバイル レポート] に設定され、[モバイル レポートを選択] オプションが [未設定] に設定されていることを示すスクリーンショット。](media/rscreatekpi-related-content-mobile-report.png)

ポータルで KPI をクリックすると、関連するコンテンツ ドロップダウンにモバイル レポートのサムネイルが表示されます。 このサムネイルをクリックすると、このレポートに直接移動できます。

また、カスタム URL を指定することもできます。 このタスクには、Web サイト、SharePoint サイト、SSRS レポートへの URL (ハードコーディングされたパラメーターを渡すことができます) のいずれでも使用できます。

![[関連するコンテンツ] オプションが [カスタム URL] に設定され、[URL を入力] オプションが [http://] に設定されていることを示すスクリーンショット。](media/rscreatekpi-related-content-custom-url.png)

KPI をクリックすると、関連するコンテンツの下に URL が表示されます。

追加できるモバイル レポートまたはカスタム URL は 1 つだけです。
  
## <a name="removing-a-kpi"></a>KPI を削除する  
  
KPI を削除するには、次の手順を実行します。
  
1. 削除する KPI の **省略記号 [...]** を選択します。 **[管理]** を選択します。  
  
    ![KPI の省略記号オプションが選択され、[管理] オプションが選択されているスクリーンショット。](../reporting-services/media/rsremovekpi1.png)  
  
2. **[削除]** を選択します。 確認ダイアログで **[削除]** を再度選択します。  
  
    ![[削除] オプションのスクリーンショット。](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>KPI を更新する  
  
KPI を更新するには、共有データセットのキャッシュを構成する必要があります。 キャッシュ更新計画の詳細については、「[共有データセットの操作](../reporting-services/work-with-shared-datasets-web-portal.md)」を参照してください。  
  
## <a name="next-steps"></a>次のステップ
  
[Web ポータル](../reporting-services/web-portal-ssrs-native-mode.md)  
[共有データセットの操作](../reporting-services/work-with-shared-datasets-web-portal.md)

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
