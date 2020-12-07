---
description: '[値包含プロファイル要求] のオプション (データ プロファイル タスク)'
title: '[値包含プロファイル要求] のオプション (データ プロファイル タスク) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: ca94da82-a4c9-4e87-9cba-c2d85bd31f01
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c30a5e35a3c3e5b8e127a317e6d44880dee2e7f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88430934"
---
# <a name="value-inclusion-profile-request-options-data-profiling-task"></a>[値包含プロファイル要求] のオプション (データ プロファイル タスク)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **[プロファイル要求]** ページの **[要求プロパティ]** ペインを使用すると、要求ペインで選択した **[値包含プロファイル要求]** のオプションを設定できます。 値包含プロファイルは、2 つの列間または列のセット間の値の重複を計算します。 したがって、このプロファイルでは、列または列のセットが、選択したテーブル間の外部キーとして適しているかどうかを判断できます。 また、このプロファイルを使用すると、無効な値などのデータの問題を特定できます。 たとえば、値包含プロファイルで Sales テーブルの ProductID 列をプロファイルするとします。 プロファイルでは、この列に Products テーブルの ProductID 列には存在しない値が含まれていることを検出できます。  
  
> [!NOTE]  
>  このトピックで説明するオプションは、 **[データ プロファイル タスク エディター]** の **[プロファイル要求]** ページに表示されます。 エディターのこのページの詳細については、「[Data Profiling Task Editor &#40;Profile Requests Page&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)」(データ プロファイル タスク エディター &#40;[プロファイル要求] ページ&#41;)を参照してください。  
  
 データ プロファイル タスクの使用方法の詳細については、「 [データ プロファイル タスクのセットアップ](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)」を参照してください。 Data Profile Viewer を使用してデータ プロファイル タスクの出力を分析する方法の詳細については、「 [Data Profile Viewer](../../integration-services/control-flow/data-profile-viewer.md)」を参照してください。  
  
## <a name="understanding-the-selection-of-columns-for-the-inclusioncolumns-property"></a>InclusionColumns プロパティの列の選択について  
 **[値包含プロファイル要求]** は、サブセット内のすべての値がスーパーセット内に存在するかどうかを計算します。 多くの場合、スーパーセットは参照テーブルです。 たとえば、住所テーブルの州列はサブセット テーブルです。 この列の 2 文字の州コードはすべて、スーパーセット テーブルである米国郵便サービス州コード テーブルにも存在します。  
  
 サブセット列またはスーパーセット列の値として [(*)] ワイルドカードを使用する場合、データ プロファイル タスクは、一方の側の各列ともう一方の側の指定された列を比較します。  
  
> [!NOTE]  
>  [(*)] を選択した場合、多数の計算が実行され、タスクのパフォーマンスが低下する可能性があります。  
  
## <a name="understanding-the-threshold-settings"></a>しきい値設定について  
 2 つの異なるしきい値設定を使用すると、[値包含プロファイル要求] の出力を絞り込むことができます。  
  
 **[InclusionThresholdSetting]** で **[None]** 以外の値を指定した場合、値包含プロファイルは、次のいずれかの条件に該当する場合にのみスーパーセット内のサブセットの包含の強さを報告します。  
  
-   包含の強さが **[InclusionStrengthThreshold]** で指定されたしきい値を超える場合。  
  
-   包含の強さの値が 1.0 で、 **[InclusionStrengthThreshold]** が **[Exact]** に設定されている場合。  
  
 値が一意でないためにスーパーセット列がスーパーセット テーブルの適切なキーではない組み合わせをフィルターで除外することにより、出力をさらに絞り込むことができます。 **[SupersetColumnsKeyThresholdSetting]** で **[None]** 以外の値を指定した場合、値包含プロファイルは、次のいずれかの条件に該当する場合にのみスーパーセット内のサブセットの包含の強さを報告します。  
  
-   スーパーセット テーブルでのスーパーセット列のキー適合性が **[SupersetColumnsKeyThreshold]** で指定されたしきい値を超える場合。  
  
-   包含の強さの値が 1.0 で、 **[SupersetColumnsKeyThreshold]** が **[Exact]** に設定されている場合。  
  
## <a name="request-properties-options"></a>[要求プロパティ] のオプション  
 **[要求プロパティ]** ペインに表示される **[値包含プロファイル要求]** のオプション グループは次のとおりです。  
  
-   **[データ]**( **[SubsetTableOrView]** オプション、 **[SupersetTableOrView]** オプション、 **[InclusionColumns]** オプションなど)  
  
-   **全般**  
  
-   **[オプション]**  
  
### <a name="data-options"></a>[データ] のオプション  
 **[ConnectionManager]**  
 プロファイル対象のテーブルまたはビューを含む [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データベースに接続するには、.NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) を使用する既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続マネージャーを選択します。  
  
 **[SubsetTableOrView]**  
 プロファイル対象の既存のテーブルまたはビューを選択します。  
  
 詳細については、このトピックの「[SubsetTableOrView] および [SupersetTableOrView] のオプション」を参照してください。  
  
 **[SupersetTableOrView]**  
 プロファイル対象の既存のテーブルまたはビューを選択します。  
  
 詳細については、このトピックの「[SubsetTableOrView] および [SupersetTableOrView] のオプション」を参照してください。  
  
 **[InclusionColumns]**  
 サブセット テーブルとスーパーセット テーブルから列または列のセットを選択します。  
  
 詳細については、このトピックの「InclusionColumns プロパティの列の選択について」と「[InclusionColumns] のオプション」を参照してください。  
  
#### <a name="subsettableorview-and-supersettableorview-options"></a>[SubsetTableOrView] および [SupersetTableOrView] のオプション  
 **[スキーマ]**  
 選択したテーブルが属するスキーマを指定します。 このオプションは読み取り専用です。  
  
 **[TableOrView]**  
 選択したテーブルの名前を表示します。 このオプションは読み取り専用です。  
  
#### <a name="inclusioncolumns-options"></a>[InclusionColumns] のオプション  
 次のオプションは、 **[InclusionColumns]** で選択したプロファイル対象の各列のセットで使用できます。  
  
 詳細については、このトピックの「InclusionColumns プロパティの列の選択について」を参照してください。  
  
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
 **[None]**  
 プロファイルの出力を絞り込むためのしきい値設定を選択します。 このプロパティの既定値は **[Specified]** です。 詳細については、このトピックの「しきい値設定について」を参照してください。  
  
|値|説明|  
|-----------|-----------------|  
|**なし**|しきい値を指定しません。 キーの強さは、その値に関係なく報告されます。|  
|**[Specified]**|**[InclusionStrengthThreshold]** で指定したしきい値を使用します。 包含の強さは、このしきい値より大きい場合にのみ報告されます。|  
|**[Exact]**|しきい値を指定しません。 包含の強さは、サブセットの値がスーパーセットの値に完全に含まれている場合にのみ報告されます。|  
  
 **[InclusionStrengthThreshold]**  
 0 ～ 1 の値を使用して、包含の強さが報告されるしきい値を指定します。 このプロパティの既定値は 0.95 です。 このオプションは、 **[InclusionThresholdSetting]** で **[Specified]** が選択されている場合にのみ有効です。  
  
 詳細については、このトピックの「しきい値設定について」を参照してください。  
  
 **[None]**  
 スーパーセットのしきい値を指定します。 このプロパティの既定値は **[Specified]** です。 詳細については、このトピックの「しきい値設定について」を参照してください。  
  
|値|説明|  
|-----------|-----------------|  
|**なし**|しきい値を指定しません。 包含の強さは、スーパーセット列のキーの強さに関係なく報告されます。|  
|**[Specified]**|**[SupersetColumnsKeyThreshold]** で指定したしきい値を使用します。 包含の強さは、スーパーセット列のキーの強さがこのしきい値より大きい場合にのみ報告されます。|  
|**[Exact]**|しきい値を指定しません。 包含の強さは、スーパーセット列がスーパーセット テーブルのキーに完全に一致している場合にのみ報告されます。|  
  
 **[SupersetColumnsKeyThreshold]**  
 0 ～ 1 の値を使用して、包含の強さが報告されるしきい値を指定します。 このプロパティの既定値は 0.95 です。 このオプションは、 **[SupersetColumnsKeyThresholdSetting]** で **[Specified]** が選択されている場合にのみ有効です。  
  
 詳細については、このトピックの「しきい値設定について」を参照してください。  
  
 **[MaxNumberOfViolations]**  
 出力で報告する包含違反の最大数を指定します。 このプロパティの既定値は 100 です。 **[InclusionThresholdSetting]** で **[Exact]** が選択されている場合、このオプションは無効です。  
  
## <a name="see-also"></a>関連項目  
 [データ プロファイル タスク エディター ([全般] ページ)](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [単一テーブル クイック プロファイル フォーム &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
