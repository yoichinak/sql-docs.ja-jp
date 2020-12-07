---
description: '[候補キー プロファイル要求] のオプション (データ プロファイル タスク)'
title: '[候補キー プロファイル要求] のオプション (データ プロファイル タスク) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 8632dbc4-4394-4dc7-b19c-f9adeb21ba52
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 499f56a0ce11bc68ad046035ff0a43d80ae4bfe7
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123586"
---
# <a name="candidate-key-profile-request-options-data-profiling-task"></a>[候補キー プロファイル要求] のオプション (データ プロファイル タスク)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **[プロファイル要求]** ページの **[要求プロパティ]** ペインを使用すると、要求ペインで選択した **[候補キー プロファイル要求]** のオプションを設定できます。 候補キー プロファイルは、列または列のセットが、選択したテーブルのキーまたは近似キーであるかどうかを報告します。 また、このプロファイルを使用すると、キーとなる可能性がある列の重複値などのデータの問題を特定できます。  
  
> [!NOTE]  
>  このトピックで説明するオプションは、 **[データ プロファイル タスク エディター]** の **[プロファイル要求]** ページに表示されます。 エディターのこのページの詳細については、「[Data Profiling Task Editor &#40;Profile Requests Page&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)」(データ プロファイル タスク エディター &#40;[プロファイル要求] ページ&#41;)を参照してください。  
  
 データ プロファイル タスクの使用方法の詳細については、「 [データ プロファイル タスクのセットアップ](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)」を参照してください。 Data Profile Viewer を使用してデータ プロファイル タスクの出力を分析する方法の詳細については、「 [Data Profile Viewer](../../integration-services/control-flow/data-profile-viewer.md)」を参照してください。  
  
## <a name="understanding-the-selection-of-columns-for-the-keycolumns-property"></a>KeyColumns プロパティの列の選択について  
 各 **候補キー プロファイル要求** は、1 つまたは複数の列で構成される単一のキー候補のキーの強さを計算します。  
  
-   **[KeyColumns]** で列を 1 つだけ選択すると、その列のキーの強さが計算されます。  
  
-   **[KeyColumns]** で複数の列を選択すると、選択したすべての列で構成される複合キーのキーの強さが計算されます。  
  
-   **[KeyColumns]** でワイルドカード文字 **[(\*)]** を選択すると、テーブルまたはビューの各列のキーの強さが計算されます。  
  
 たとえば、A 列、B 列、および C 列を含むサンプル テーブルについて考えてみます。 **[KeyColumns]** について次の選択を行います。  
  
-   \*[KeyColumns] **で [(**)] と C 列を選択します。 タスクは、C 列のキーの強さを計算し、次に複合キー候補 (A 列と C 列の組み合わせと B 列と C 列の組み合わせ) のキーの強さを計算します。  
  
-   \*[KeyColumns]\*で [( **)] と [(**)] を選択します。 タスクは、A 列、B 列、および C 列のキーの強さを個別に計算し、次に複合キー候補 (A, B)、(A, C)、および (B, C) のキーの強さを計算します。  
  
> [!NOTE]  
>  [(*)] を選択した場合、多数の計算が実行され、タスクのパフォーマンスが低下する可能性があります。 ただし、キーのしきい値を満たすサブセットをタスクが見つけた場合、その他の組み合わせは分析されません。 たとえば、上記のサンプル テーブルで C 列がキーであるとタスクが判断した場合、複合キー候補の分析は続行されません。  
  
## <a name="request-properties-options"></a>[要求プロパティ] のオプション  
 **[要求プロパティ]** ペインに表示される **[候補キー プロファイル要求]** のオプション グループは次のとおりです。  
  
-   **[データ]**( **[TableOrView]** オプション、 **[KeyColumns]** オプションなど)  
  
-   **全般**  
  
-   **[オプション]**  
  
### <a name="data-options"></a>[データ] のオプション  
 **[ConnectionManager]**  
 プロファイル対象のテーブルまたはビューを含む [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データベースに接続するには、.NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) を使用する既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続マネージャーを選択します。  
  
 **[TableOrView]**  
 プロファイル対象の既存のテーブルまたはビューを選択します。  
  
 詳細については、このトピックの「[TableorView] のオプション」を参照してください。  
  
 **[KeyColumns]**  
 プロファイル対象の既存の列を選択します。 すべての列をプロファイルするには、 **[(\*)]** を選択します。  
  
 詳細については、このトピックの「KeyColumns プロパティの列の選択について」と「[KeyColumns] のオプション」を参照してください。  
  
#### <a name="tableorview-options"></a>[TableOrView] のオプション  
 **[スキーマ]**  
 選択したテーブルが属するスキーマを指定します。 このオプションは読み取り専用です。  
  
 **Table**  
 選択したテーブルの名前を表示します。 このオプションは読み取り専用です。  
  
#### <a name="keycolumns-options"></a>[KeyColumns] のオプション  
 次のオプションは、**[KeyColumns]** で選択したプロファイル対象の各列および **[(\*)]** オプションで使用できます。  
  
 詳細については、このトピックの「KeyColumns プロパティの列の選択について」を参照してください。  
  
 **[IsWildCard]**  
 **[(\*)]** ワイルドカードが選択されているかどうかを示します。 **[(\*)]** を選択してすべての列をプロファイルする場合、このオプションは **[True]** に設定されます。 個々の列をプロファイル対象として選択した場合、このオプションは **[False]** になります。 このオプションは読み取り専用です。  
  
 **[ColumnName]**  
 選択した列の名前を表示します。 **[(\*)]** を選択してすべての列をプロファイルする場合、このオプションは空白になります。 このオプションは読み取り専用です。  
  
 **[StringCompareOptions]**  
 文字列値を比較するためのオプションを選択します。 このプロパティのオプションを次の表に示します。 このオプションの既定値は **[Default]** です。  
  
> [!NOTE]  
>  **[ColumnName]** に **[(\*)]** ワイルドカードを使用する場合、 **[CompareOptions]** は読み取り専用で、 **[Default]** に設定されます。  
  
|値|説明|  
|-----------|-----------------|  
|**[Default]**|ソース テーブル内の列の照合順序に基づいてデータを並べ替えて比較します。|  
|**[BinarySort]**|文字ごとに定義されているビット パターンに基づいてデータを並べ替えて比較します。 バイナリ並べ替え順では、大文字と小文字が区別され、アクセントが区別されます。 また、バイナリは最速の並べ替え順です。|  
|**[DictionarySort]**|関連する言語またはアルファベットの辞書で定義されている並べ替えおよび比較ルールに基づいてデータを並べ替えて比較します。|  
  
 **[DictionarySort]** を選択した場合は、次の表に示すオプションの任意の組み合わせも選択できます。 既定では、これらの追加オプションは選択されていません。  
  
|値|説明|  
|-----------|-----------------|  
|**IgnoreCase**|比較時に、大文字と小文字を区別するかどうかを示します。 このオプションを設定した場合、文字列比較で大文字と小文字は区別されません。 たとえば、"ABC" は "abc" と同一になります。|  
|**IgnoreNonSpace**|比較で、通常の文字と分音文字付きの文字を区別するかどうかを指定します。 このオプションを設定した場合、比較で分音文字は無視されます。 たとえば、"Ã¥" は "a" に等しくなります。|  
|**IgnoreKanaType**|日本語の比較で、2 種類のかな文字である、ひらがなとカタカナを区別するかどうかを指定します。 このオプションを設定した場合、文字列比較でひらがなとカタカナは区別されません。|  
|**IgnoreWidth**|比較で、1 バイト文字と、それと同じ文字を表記した 2 バイト文字を区別するかどうかを指定します。 このオプションを設定した場合、文字列比較で 1 バイト表記と 2 バイト表記は同一文字として扱われます。|  
  
### <a name="general-options"></a>[全般] のオプション  
 **RequestID**  
 このプロファイル要求を識別するわかりやすい名前を入力します。 通常、自動生成された値を変更する必要はありません。  
  
### <a name="options"></a>オプション  
 **[ThresholdSetting]**  
 このプロパティのオプションを次の表に示します。 このプロパティの既定値は **[Specified]** です。  
  
|値|説明|  
|-----------|-----------------|  
|**なし**|しきい値が指定されていません。 キーの強さは、その値に関係なく報告されます。|  
|**[Specified]**|しきい値は **[KeyStrengthThreshold]** で指定します。 キーの強さは、このしきい値より大きい場合にのみ報告されます。|  
|**[Exact]**|しきい値が指定されていません。 キーの強さは、選択した列がキーに完全に一致している場合にのみ報告されます。|  
  
 **[KeyStrengthThreshold]**  
 0 ～ 1 の値を使用して、キーの強さが報告されるしきい値を指定します。 このプロパティの既定値は 0.95 です。 このオプションは、 **[KeyStrengthThresholdSetting]** で **[Specified]** が選択されている場合にのみ有効です。  
  
 **[MaxNumberOfViolations]**  
 出力で報告する候補キー違反の最大数を指定します。 このプロパティの既定値は 100 です。 このオプションは、 **[KeyStrengthThresholdSetting]** で **[Exact]** が選択されている場合は無効です。  
  
## <a name="see-also"></a>関連項目  
 [データ プロファイル タスク エディター ([全般] ページ)](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [単一テーブル クイック プロファイル フォーム &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
