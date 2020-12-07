---
description: Data Profile Viewer (Data Profile Viewer)
title: Data Profile Viewer | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 19b96ce10fc5579e86fde10b4c3331b0da060050
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724963"
---
# <a name="data-profile-viewer"></a>Data Profile Viewer (Data Profile Viewer)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  データのプロファイル処理では、次に、データ プロファイルを表示して分析します。 このプロファイルは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ内でデータ プロファイル タスクを実行してデータ プロファイルを計算した後に表示できます。 データ プロファイル タスクの設定方法および実行方法の詳細については、「 [データ プロファイル タスクのセットアップ](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  出力ファイルには、データベースに関する機密データやデータベースに格納されているデータが含まれる場合があります。 このファイルの安全性を高める方法の推奨事項については、「 [パッケージで使用されるファイルへのアクセス](../../integration-services/security/security-overview-integration-services.md#files)」をご覧ください。  
  
## <a name="data-profiles"></a>データのプロファイル  
 データ プロファイルを表示するには、出力をファイルに送信するようにデータ プロファイル タスクを構成し、スタンドアロンの Data Profile Viewer を使用します。 Data Profile Viewer を開くには、次のいずれかの操作を行います。  
  
-   **デザイナーの** [データ プロファイル] [!INCLUDE[ssIS](../../includes/ssis-md.md)] でタスクを右クリックし、 **[編集]** をクリックします。 **データ プロファイル タスク エディター** の **[全般]** ページで、 **[プロファイル ビューアーを開く]** をクリックします。  
  
-   *\<drive>* :\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn フォルダーの DataProfileViewer.exe を実行します。  
  
 このビューアーでは、複数のペインを使用して、要求したプロファイルと計算結果が表示されます。また、詳細情報を表示するための機能やドリル ダウン機能をオプションで使用できます。  
  
 **[プロファイル]** ペイン  
 **[プロファイル]** ペインには、データ プロファイル タスクで要求されたプロファイルが表示されます。 **[プロファイル]** ペインでプロファイルを選択すると、プロファイルの計算結果がビューアーの他のペインに表示されます。  
  
 **[結果]** ペイン  
 **[結果]** ペインでは、プロファイルの計算結果が 1 行にまとめられます。 たとえば、 **[列長分布プロファイル]** を要求すると、この行には最小長、最大長、および行数が表示されます。 ほとんどのプロファイルでは、 **[結果]** ペインでこの行を選択すると、オプションの **[詳細]** ペインに追加の詳細を表示できます。  
  
 **[詳細]** ペイン  
 ほとんどの種類のプロファイルの **[詳細]** ペインには、 **[結果]** ペインで選択したプロファイルの結果に関する追加情報が表示されます。 たとえば、 **[列長分布プロファイル]** を要求すると、 **[詳細]** ペインには検出された各列の長さが表示されます。 また、列の値の長さがこのペインに表示された列の長さである行の数および割合も表示されます。  
  
 複数の列に対して計算される 3 種類のプロファイル (候補キー、機能依存、および値包含) の **[詳細]** ペインには、想定されているリレーションシップの違反が表示されます。 たとえば、[候補キー プロファイル] を要求すると、[詳細] ペインには候補キーの一意性に違反している重複値が表示されます。  
  
 プロファイルの計算に使用したデータ ソースが使用可能な場合、 **[詳細]** ペインの行をダブルクリックすると、 **[ドリル ダウン]** ペインに、一致するデータ行を表示できます。  
  
 **[ドリル ダウン]** ペイン  
 次の条件に当てはまる場合、 **[詳細]** ペインの行をダブルクリックすると、 **[ドリル ダウン]** ペインに、一致するデータ行を表示できます。  
  
-   計算に使用したデータ ソースが利用可能であること。  
  
-   データを表示する権限があること。  
  
 Data Profile Viewer では、ドリル ダウン要求のためのソース データベースへの接続に、Windows 認証と現在のユーザーの資格情報が使用されます。 データ プロファイル タスクを実行したパッケージに格納されている接続情報は使用されません。  
  
> [!IMPORTANT]  
>  Data Profile Viewer に用意されているドリル ダウン機能は、元のデータ ソースにライブ クエリを送信します。 これらのクエリは、サーバーのパフォーマンスに悪影響を及ぼす場合があります。  
>   
>  最近作成されたものではない出力ファイルからドリル ダウンした場合、ドリルダウン クエリは、元の出力の計算に使用された行セットとは異なる行セットを返す場合があります。  
  
 Data Profile Viewer のユーザー インターフェイスの詳細については、「 [Data Profile Viewer の F1 ヘルプ]()」をご覧ください。  
  
## <a name="data-profile-viewer-f1-help"></a>Data Profile Viewer の F1 ヘルプ
  Data Profile Viewer を使用すると、データ プロファイル タスクの出力を表示できます。  
  
 Data Profile Viewer の使用方法の詳細については、「 [Data Profile Viewer](../../integration-services/control-flow/data-profile-viewer.md)」を参照してください。 データ プロファイル タスクの使用方法の詳細については、「 [データ プロファイル タスクのセットアップ](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)」を参照してください。データ プロファイル タスクを使用すると、Data Profile Viewer で分析するプロファイル出力を作成できます。  
  
### <a name="static-options"></a>静的オプション  
 **[ファイル]**  
 データ プロファイル タスクの出力を含む保存済みファイルを参照する場合にクリックします。  
  
 **[プロファイル]** ペイン  
 出力に含まれるプロファイルを表示するには、 **[プロファイル]** ペインのツリーを展開します。 プロファイルを選択し、そのプロファイルの結果を表示します。  
  
 **[メッセージ]** ペイン  
 状態を示すメッセージが表示されます。  
  
 **[ドリル ダウン]** ペイン  
 データ プロファイル タスクで使用されるデータ ソースが使用可能な場合は、出力の値と一致するデータの行が表示されます。  
  
 たとえば、US State 列に対する列の値分布プロファイルの出力を表示している場合に、 **[詳細な値分布]** ペインに "WA" の行が含まれているとします。 **[詳細な値分布]** ペインでこの行をダブルクリックすると、State 列が "WA" であるデータの行が [ドリル ダウン] ペインに表示されます。  
  
### <a name="dynamic-options"></a>動的オプション  
  
#### <a name="profile-type--column-length-distribution-profile"></a>プロファイルの種類 = 列長分布プロファイル  
  
##### <a name="column-length-distribution-profile---column-pane"></a>列長分布プロファイル - \<column> ペイン  
 **[最小の長さ]**  
 この列の最小の長さが表示されます。  
  
 **[最大の長さ]**  
 この列の最大の長さが表示されます。  
  
 **[先頭のスペースを無視する]**  
 **IgnoreLeadingSpaces** の値に True または False のいずれを使用してこのプロファイルが計算されたかが表示されます。 このプロパティは、[データ プロファイル タスク エディター] の **[プロファイル要求]** ページで設定されています。  
  
 **[末尾のスペースを無視する]**  
 **IgnoreTrailingSpaces** の値に True または False のいずれを使用してこのプロファイルが計算されたかが表示されます。 このプロパティは、[データ プロファイル タスク エディター] の **[プロファイル要求]** ページで設定されています。  
  
 **行数**  
 テーブルまたはビューの行数が表示されます。  
  
##### <a name="detailed-length-distribution-pane"></a>[詳細な長さ分布] ペイン  
 **[データ型]**  
 プロファイルされた列の列長が表示されます。  
  
 **Count**  
 プロファイルされた列の値の長さが **[長さ]** 列に表示された長さである行の数が表示されます。  
  
 **Percentage**  
 プロファイルされた列の値の長さが **[長さ]** 列に表示された長さである行の割合が表示されます。  
  
#### <a name="profile-type--column-null-ratio-profile"></a>プロファイルの種類 = 列の NULL 比プロファイル  
  
##### <a name="column-null-ratio-profile---column-pane"></a>列の NULL 比プロファイル - \<column> ペイン  
 **[NULL カウント]**  
 プロファイルされた列が NULL 値である行の数が表示されます。  
  
 **[NULL 比率]**  
 プロファイルされた列が NULL 値である行の割合が表示されます。  
  
 **行数**  
 テーブルまたはビューの行数が表示されます。  
  
#### <a name="profile-type--column-pattern-profile"></a>プロファイルの種類 = 列パターン プロファイル  
  
##### <a name="column-pattern-profile---column-pane"></a>列パターン プロファイル - \<column> ペイン  
 **行数**  
 テーブルまたはビューの行数が表示されます。  
  
##### <a name="pattern-distribution-pane"></a>[パターン分布] ペイン  
 **パターン**  
 プロファイルされた列について計算されたパターンが表示されます。  
  
 **Percentage**  
 **[パターン]** 列に表示されたパターンに一致する値を持つ行の割合が表示されます。  
  
#### <a name="profile-type--column-statistics-profile"></a>プロファイルの種類 = 列統計プロファイル  
  
##### <a name="column-statistics-profile---column-pane"></a>列統計プロファイル - \<column> ペイン  
 **最小**  
 プロファイルされた列の最小値が表示されます。  
  
 **[最大]**  
 プロファイルされた列の最大値が表示されます。  
  
 **Mean (平均値)**  
 プロファイルされた列の値の平均が表示されます。  
  
 **Standard Deviation**  
 プロファイルされた列の値の標準偏差が表示されます。  
  
#### <a name="profile-type--column-value-distribution-profile"></a>プロファイルの種類 = 列の値分布プロファイル  
  
##### <a name="column-value-distribution-profile---column-pane"></a>列の値分布プロファイル - \<column> ペイン  
 **[個別の値数]**  
 プロファイルされた列の個別の値数が表示されます。  
  
 **行数**  
 テーブルまたはビューの行数が表示されます。  
  
##### <a name="detailed-value-distribution-pane"></a>[詳細な値分布] ペイン  
 **Value**  
 プロファイルされた列の個別の値が表示されます。  
  
 **Count**  
 プロファイルされた列の値が **[値]** 列に表示された値である行の数が表示されます。  
  
 **Percentage**  
 プロファイルされた列の値が **[値]** 列に表示された値である行の割合が表示されます。  
  
#### <a name="profile-type--candidate-key-profile"></a>プロファイルの種類 = 候補キー プロファイル  
  
##### <a name="candidate-key-profile---table-pane"></a>候補キー プロファイル - \<table> ペイン  
 **[キー列]**  
 プロファイル対象の候補キーとして選択した列が表示されます。  
  
 **[キーの強さ]**  
 候補キーの列または列の組み合わせの強さがパーセンテージで表示されます。 キーの強さが 100% 未満である場合は、重複する値が存在することを示します。  
  
##### <a name="key-violations-pane"></a>[キー違反] ペイン  
 **\<column1>、\<column2> などです。**  
 プロファイルされた列で見つかった重複する値が表示されます。  
  
 **Count**  
 指定された列の値が最初の列に表示された値である行の数が表示されます。  
  
#### <a name="profile-type--functional-dependency-profile"></a>プロファイルの種類 = 機能依存プロファイル  
  
##### <a name="functional-dependency-profile-pane"></a>[機能依存プロファイル] ペイン  
 **[決定列]**  
 決定列として選択した列が表示されます。 米国郵便番号によって州が一意に決定される例の場合、郵便番号は決定列です。  
  
 **[依存列]**  
 依存列として選択した列が表示されます。 米国郵便番号によって州が一意に決定される例の場合、州は依存列です。  
  
 **[機能依存の強さ]**  
 列間の機能依存の強さがパーセンテージで表示されます。 キーの強さが 100% 未満である場合は、決定値によって依存値が決定されないケースがあることを示します。 米国郵便番号によって州が一意に決定される例でキーの強さが 100% 未満である場合は、無効な値が州の列に含まれていることを示します。  
  
##### <a name="functional-dependency-violations-pane"></a>[機能依存違反] ペイン  
  
> [!NOTE]  
>  データに含まれるエラー値の割合が高いと、機能依存プロファイルの結果が予期しない結果になることがあります。 たとえば、"98052" という郵便番号の値に対応する州の値として "WI" という値が 90% の行に含まれている場合、 機能依存プロファイルにより、正しい州の値である "WA" という値の行が違反として報告されます。  
  
 **\<determinant column name>**  
 違反が検出された機能依存の決定列または列の組み合わせの値が表示されます。  
  
 **\<dependent column name>**  
 違反が検出された機能依存の依存列の値が表示されます。  
  
 **サポート数 (Support Count)**  
 決定列の値によって依存列が決定される行の数が表示されます。  
  
 **[違反カウント]**  
 決定列の値によって依存列が決定されない行の数が表示されます (依存値が **\<dependent column name>** 列に表示された値である行)。  
  
 **サポート比率 (Support Percentage)**  
 決定列によって依存列が決定される行の割合が表示されます。  
  
#### <a name="profile-type--value-inclusion-profile"></a>プロファイルの種類 = 値包含プロファイル  
  
##### <a name="value-inclusion-profile-pane"></a>[値包含プロファイル] ペイン  
 **[サブセット側の列]**  
 スーパーセット列の一部であるかどうかを判断するためにプロファイルされた列または列の組み合わせが表示されます。  
  
 **[スーパーセット側の列]**  
 サブセット列の値が含まれているかどうかを判断するためにプロファイルされた列または列の組み合わせが表示されます。  
  
 **[包含の強さ]**  
 列間の重複の強さがパーセンテージで表示されます。 キーの強さが 100% 未満である場合は、サブセットの値がスーパーセットの値の中に含まれていないケースがあることを示します。  
  
##### <a name="inclusion-violations-pane"></a>[包含違反] ペイン  
 **\<column1>、\<column2> などです。**  
 スーパーセット列に含まれていないサブセット列の値が表示されます。  
  
 **Count**  
 指定された列の値が最初の列に表示された値である行の数が表示されます。  
