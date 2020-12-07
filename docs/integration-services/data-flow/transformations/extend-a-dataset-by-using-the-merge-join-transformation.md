---
description: マージ結合変換を使用してデータセットを拡張する
title: マージ結合変換を使用してデータセットを拡張する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Merge Join transformation
- datasets [Integration Services], joining
- datasets [Integration Services], extending
- joining datasets [Integration Services]
ms.assetid: 9e512c3c-f89b-45f3-8281-cdb8f35a2b1f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7000b1593f20305c4d09f1f8ee11eb4b874ee3aa
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123353"
---
# <a name="extend-a-dataset-by-using-the-merge-join-transformation"></a>マージ結合変換を使用してデータセットを拡張する

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  マージ結合変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと、マージ結合変換への入力を提供する 2 つのデータ フロー コンポーネントがあらかじめ含まれている必要があります。  
  
 マージ結合変換には、2 つの並べ替え済み入力が必要です。 詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。  
  
### <a name="to-extend-a-dataset"></a>データセットを拡張するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、マージ結合変換をデザイン画面にドラッグします。  
  
4.  マージ結合変換をデータ フローに連結します。連結するには、データ ソースまたは直前の変換からマージ結合変換にコネクタをドラッグします。  
  
5.  マージ結合変換をダブルクリックします。  
  
6.  **[マージ結合変換エディター]** ダイアログ ボックスで、 **[結合の種類]** ボックスの一覧から使用する結合の種類を選択します。  
  
    > [!NOTE]  
    >  **[左外部結合]** を選択した場合、 **[入力の入れ替え]** をクリックして入力を切り替え、左外部結合を右外部結合に変換できます。  
  
7.  左辺の入力内の列を、右辺の入力内の列にドラッグし、結合列を指定します。 列の名前が同じ場合、 **[結合キー]** チェック ボックスをオンにすると、マージ結合変換は自動的に結合を作成できます。  
  
    > [!NOTE]  
    >  並べ替えの位置が同じ列のみの結合を作成できます。この場合、並べ替えの位置によって指定された順序で結合を作成する必要があります。 順序が正しくない結合を作成しようとすると、 **[マージ結合変換エディター]** で、スキップした並べ替えの位置に対して、追加の結合を作成するように要求されます。  
  
    > [!NOTE]  
    >  既定では、出力は結合列に基づいて並べ替えられます。  
  
8.  左辺の入力および右辺の入力で、出力に追加して含める列のチェック ボックスをオンにします。 結合列は、既定で含まれています。  
  
9. 必要に応じて、 **[出力の別名]** 列で出力列の名前を更新します。  
  
10. **[OK]** をクリックします。  
  
11. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [マージ結合変換](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../../integration-services/data-flow/integration-services-paths.md)   
 [データ フロー タスク](../../../integration-services/control-flow/data-flow-task.md)  
  
  
