---
description: '[列パターン プロファイル要求] のオプション (データ プロファイル タスク)'
title: '[列パターン プロファイル要求] のオプション (データ プロファイル タスク) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 9ccb8fc5-f65e-41a2-9511-7fa55586eb8b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 85beabd085481a48d6681bbaf2d2d381a1d0df93
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123555"
---
# <a name="column-pattern-profile-request-options-data-profiling-task"></a>[列パターン プロファイル要求] のオプション (データ プロファイル タスク)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **[プロファイル要求]** ページの **[要求プロパティ]** ペインを使用すると、要求ペインで選択した **[列パターン プロファイル要求]** のオプションを設定できます。 列パターン プロファイルは、文字列型の列に含まれる指定された比率の値に対応する一連の正規表現を報告します。 このプロファイルを使用すると、無効な文字列などのデータの問題を特定できます。また、このプロファイルには、新しい値を検証するために将来使用できる正規表現も提示されます。 たとえば、米国郵便番号列のパターン プロファイルでは、\d{5}-\d{4}、\d{5}、および \d{9} という正規表現が生成されます。 その他の正規表現が示された場合、データに無効な値または形式が正しくない値が含まれている可能性があります。  
  
> [!NOTE]  
>  このトピックで説明するオプションは、 **[データ プロファイル タスク エディター]** の **[プロファイル要求]** ページに表示されます。 エディターのこのページの詳細については、「[Data Profiling Task Editor &#40;Profile Requests Page&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)」(データ プロファイル タスク エディター &#40;[プロファイル要求] ページ&#41;)を参照してください。  
  
 データ プロファイル タスクの使用方法の詳細については、「 [データ プロファイル タスクのセットアップ](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)」を参照してください。 Data Profile Viewer を使用してデータ プロファイル タスクの出力を分析する方法の詳細については、「 [Data Profile Viewer](../../integration-services/control-flow/data-profile-viewer.md)」を参照してください。  
  
## <a name="understanding-the-use-of-delimiters-and-symbols"></a>区切り記号と記号の使用方法について  
 データ プロファイル タスクは、 **列パターン プロファイル要求** のパターンを計算する前にデータをトークン化します。 つまり、データ プロファイル タスクは、文字列値をトークンと呼ばれる小さな単位に分割します。 データ プロファイル タスクは、 **Delimiters** プロパティおよび **Symbols** プロパティで指定された区切り記号と記号に基づいて文字列をトークンに分割します。  
  
-   **Delimiters** 既定では、区切り記号の一覧には、空白文字、水平タブ文字 (\t)、改行文字 (\n)、および復帰文字 (\r) が含まれます。 追加の区切り記号を指定できますが、既定の区切り記号を削除することはできません。  
  
-   **Symbols** 既定では、**[Symbols]** の一覧には、`,.;:-"'~=&/@!?()<>[]{}|#*^%` と目盛が含まれます。 たとえば、記号が "`()-`" の場合、値 "(425) 123-4567" は ["(", "425", ")", "123", "-", "4567", ")"] としてトークン化されます。  
  
 1 つの文字を区切り記号と記号の両方に使用することはできません。  
  
 区切り記号はすべて、トークン化処理の一部として 1 つの空白文字に正規化されます。一方、記号はそのまま保持されます。  
  
## <a name="understanding-the-use-of-the-tag-table"></a>タグ テーブルの使用方法について  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内に作成した特別なテーブルにタグと関連用語を保存することで、1 つのタグを持つ関連トークンを必要に応じてグループ化することができます。 タグ テーブルには、"Tag" および "Term" という名前の 2 つの文字列型の列が必要です。 これらの列には **char** 型、 **nchar** 型、 **varchar** 型、または **nvarchar** 型を指定できますが、 **text** 型と **ntext** 型は指定できません。 1 つのテーブルで複数のタグと対応する用語を結合できます。 1 つの列パターン プロファイル要求で使用できるタグ テーブルは 1 つのみです。 タグ テーブルには個別の [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを使用して接続できます。 そのため、タグ テーブルは、ソース データとは異なるデータベースまたはサーバーに格納できます。  
  
 たとえば、住所に含まれる可能性がある "East"、"West"、"North"、および "South" という値を、"Direction" という 1 つのタグでグループ化できます。 次の表に、このようなタグ テーブルの例を示します。  
  
|タグ|期間|  
|---------|----------|  
|Direction|East|  
|Direction|West|  
|Direction|North|  
|Direction|South|  
  
 別のタグを使用して、住所の "通り" の概念を表すさまざまな単語をグループ化できます。  
  
|タグ|期間|  
|---------|----------|  
|Street|Street|  
|Street|Avenue|  
|Street|場所|  
|Street|方法|  
  
 これらのタグの組み合わせに基づいて生成される住所のパターンは次のようになります。  
  
 `\d+\ LookupTag=Direction \d+\p{L}+\ LookupTag=Street`  
  
> [!NOTE]  
>  タグ テーブルを使用すると、データ プロファイル タスクのパフォーマンスが低下します。 使用するタグは 10 個以内にし、また用語は 1 つのタグにつき 100 個以内にしてください。  
  
 同じ用語を複数のタグに関連付けることができます。  
  
## <a name="request-properties-options"></a>[要求プロパティ] のオプション  
 **[要求プロパティ]** ペインに表示される **[列パターン プロファイル要求]** のオプション グループは次のとおりです。  
  
-   **[データ]**( **[TableOrView]** オプション、 **[Column]** オプションなど)  
  
-   **全般**  
  
-   **[オプション]**  
  
### <a name="data-options"></a>[データ] のオプション  
 **[ConnectionManager]**  
 プロファイル対象のテーブルまたはビューを含む [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データベースに接続するには、.NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) を使用する既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続マネージャーを選択します。  
  
 **[TableOrView]**  
 プロファイル対象の列を含む既存のテーブルまたはビューを選択します。  
  
 詳細については、このトピックの「[TableorView] のオプション」を参照してください。  
  
 **列**  
 プロファイル対象の既存の列を選択します。 すべての列をプロファイルするには、 **[(\*)]** を選択します。  
  
 詳細については、このトピックの「[列] のオプション」を参照してください。  
  
#### <a name="tableorview-options"></a>[TableOrView] のオプション  
 **[スキーマ]**  
 選択したテーブルが属するスキーマを指定します。 このオプションは読み取り専用です。  
  
 **Table**  
 選択したテーブルの名前を表示します。 このオプションは読み取り専用です。  
  
#### <a name="column-options"></a>[列] のオプション  
 **IsWildCard**  
 **[(\*)]** ワイルドカードが選択されているかどうかを示します。 **[(\*)]** を選択してすべての列をプロファイルする場合、このオプションは **[True]** に設定されます。 個々の列をプロファイル対象として選択した場合、このオプションは **[False]** になります。 このオプションは読み取り専用です。  
  
 **[ColumnName]**  
 選択した列の名前を表示します。 **[(\*)]** を選択してすべての列をプロファイルする場合、このオプションは空白になります。 このオプションは読み取り専用です。  
  
 **[StringCompareOptions]**  
 このオプションは、列パターン プロファイルには適用されません。  
  
### <a name="general-options"></a>[全般] のオプション  
 **RequestID**  
 このプロファイル要求を識別するわかりやすい名前を入力します。 通常、自動生成された値を変更する必要はありません。  
  
### <a name="options"></a>オプション  
 **[MaxNumberOfPatterns]**  
 プロファイルで計算するパターンの最大数を指定します。 このオプションの既定値は 10 です。 最大値は 100 です。  
  
 **[PercentageDataCoverageDesired]**  
 計算されたパターンでカバーするデータの割合を指定します。 このオプションの既定値は 95 (%) です。  
  
 **[CaseSensitive]**  
 パターンで大文字と小文字を区別するかどうかを示します。 このオプションの既定値は **[False]** です。  
  
 **区切り記号**  
 テキストをトークン化するときに、単語間の空白文字と同等のものとして処理する文字の一覧が表示されます。 既定では、 **[Delimiters]** の一覧には、空白文字、水平タブ文字 (\t)、改行文字 (\n)、および復帰文字 (\r) が含まれます。 追加の区切り記号を指定できますが、既定の区切り記号を削除することはできません。  
  
 詳細については、このトピックの「区切り記号と記号の使用方法について」を参照してください。  
  
 **記号**  
 パターンの一部として保持する記号の一覧が表示されます。 記号の例として、日付を表す "/"、時刻を表す ":"、電子メール アドレスを表す "\@" などがあります。 既定では、 **[Symbols]** の一覧には、`,.;:-"'~=&/@!?()<>[]{}|#*^%` が含まれます。  
  
 詳細については、このトピックの「区切り記号と記号の使用方法について」を参照してください。  
  
 **[TagTableConnectionManager]**  
 タグ テーブルを含む [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データベースに接続するには、.NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) を使用する既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続マネージャーを選択します。  
  
 詳細については、このトピックの「タグ テーブルの使用方法について」を参照してください。  
  
 **[TagTableName]**  
 "Tag" および "Term" という名前の 2 つの文字列型の列を持つ既存のタグ テーブルを選択します。  
  
 詳細については、このトピックの「タグ テーブルの使用方法について」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ プロファイル タスク エディター ([全般] ページ)](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [単一テーブル クイック プロファイル フォーム &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
