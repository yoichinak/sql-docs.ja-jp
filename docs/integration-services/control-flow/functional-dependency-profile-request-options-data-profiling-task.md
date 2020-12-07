---
description: '[機能依存プロファイル要求] のオプション (データ プロファイル タスク)'
title: '[機能依存プロファイル要求] のオプション (データ プロファイル タスク) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 6eb853aa-8016-490c-be4f-06ab8d7f5021
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1fa83e2b75860730f4e3d9b419a2ca8ca374ba31
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88393428"
---
# <a name="functional-dependency-profile-request-options-data-profiling-task"></a>[機能依存プロファイル要求] のオプション (データ プロファイル タスク)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **[プロファイル要求]** ページの **[要求プロパティ]** ペインを使用すると、要求ペインで選択した **[機能依存プロファイル要求]** のオプションを設定できます。 機能依存プロファイルは、ある列 (依存列) の値が別の列または列のセット (決定列) の値にどの程度依存しているかを報告します。 また、このプロファイルを使用すると、無効な値などのデータの問題を特定できます。 たとえば、郵便番号を含む列と米国の州を含む列の間の依存関係をプロファイルできます。 このプロファイルでは、郵便番号によって州が一意に決定されますが、依存関係の違反を検出できます。  
  
> [!NOTE]  
>  このトピックで説明するオプションは、 **[データ プロファイル タスク エディター]** の **[プロファイル要求]** ページに表示されます。 エディターのこのページの詳細については、「[Data Profiling Task Editor &#40;Profile Requests Page&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)」(データ プロファイル タスク エディター &#40;[プロファイル要求] ページ&#41;)を参照してください。  
  
 データ プロファイル タスクの使用方法の詳細については、「 [データ プロファイル タスクのセットアップ](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)」を参照してください。 Data Profile Viewer を使用してデータ プロファイル タスクの出力を分析する方法の詳細については、「 [Data Profile Viewer](../../integration-services/control-flow/data-profile-viewer.md)」を参照してください。  
  
## <a name="understanding-the-selection-of-determinant-and-dependent-columns"></a>決定列と依存列の選択について  
 **機能依存プロファイル要求** は、決定側の列または列のセット ( **DeterminantColumns** プロパティで指定) により、依存側の列 ( **DependentColumn** プロパティで指定) の値がどの程度決定されるかを計算します。 たとえば、米国の州の列は米国郵便番号の列に機能的に依存します。 つまり、郵便番号 (決定列) が "98052" である場合、州 (依存列) は必ず "Washington" になります。  
  
 決定側については、 **DeterminantColumns** プロパティで列または列のセットを指定できます。 たとえば、A 列、B 列、および C 列を含むサンプル テーブルについて考えてみます。 **DeterminantColumns** プロパティについて次の選択を行います。  
  
-   **[(\*)]** ワイルドカードを選択した場合、データ プロファイル タスクは、各列を依存関係の決定側としてテストします。  
  
-   **[(\*)]** ワイルドカードと別の列を選択した場合、データ プロファイル タスクは、列の各組み合わせを依存関係の決定側としてテストします。 たとえば、A 列、B 列、および C 列を含むサンプル テーブルについて考えてみます。**DeterminantColumns** プロパティの値に **[(\*)]** と C 列を指定した場合、データ プロファイル タスクは、A 列と C 列の組み合わせと B 列と C 列の組み合わせを依存関係の決定側としてテストします。  
  
 依存側については、**DependentColumn** プロパティで 1 つの列または **[(\*)]** ワイルドカードを指定できます。 **[(\*)]** を選択した場合、データ プロファイル タスクは、決定側の列または列のセットを各列に対してテストします。  
  
> [!NOTE]  
>  **[(\*)]** を選択した場合、多数の計算が実行され、タスクのパフォーマンスが低下する可能性があります。 ただし、機能依存のしきい値を満たすサブセットをタスクが見つけた場合、その他の組み合わせは分析されません。 たとえば、上記のサンプル テーブルで C 列が決定列であるとタスクが判断した場合、複合候補の分析は続行されません。  
  
## <a name="request-properties-options"></a>[要求プロパティ] のオプション  
 **[要求プロパティ]** ペインに表示される **[機能依存プロファイル要求]** のオプション グループは次のとおりです。  
  
-   **[データ]**( **[DeterminantColumns]** オプション、 **[DependentColumn]** オプションなど)  
  
-   **全般**  
  
-   **[オプション]**  
  
### <a name="data-options"></a>[データ] のオプション  
 **[ConnectionManager]**  
 プロファイル対象のテーブルまたはビューを含む [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データベースに接続するには、.NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) を使用する既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続マネージャーを選択します。  
  
 **[TableOrView]**  
 プロファイル対象の既存のテーブルまたはビューを選択します。  
  
 **DeterminantColumns**  
 決定列または列のセットを選択します。 つまり、依存列の値を決定する値を持つ列または列のセットを選択します。  
  
 詳細については、このトピックの「決定列と依存列の選択について」と「[DeterminantColumns] および [DependentColumn] のオプション」を参照してください。  
  
 **DependentColumn**  
 依存列を選択します。 つまり、決定側の列または列のセットの値によって決定される値を持つ列を選択します。  
  
 詳細については、このトピックの「決定列と依存列の選択について」と「[DeterminantColumns] および [DependentColumn] のオプション」を参照してください。  
  
#### <a name="determinantcolumns-and-dependentcolumn-options"></a>[DeterminantColumns] および [DependentColumn] のオプション  
 次のオプションは、 **[DeterminantColumns]** および **[DependentColumn]** で選択したプロファイル対象の各列で使用できます。  
  
 詳細については、このトピックの「決定列と依存列の選択について」を参照してください。  
  
 **IsWildCard**  
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
 しきい値設定を指定します。 このプロパティの既定値は **[Specified]** です。  
  
|値|説明|  
|-----------|-----------------|  
|**なし**|しきい値を指定しません。 機能依存の強さは、その値に関係なく報告されます。|  
|**[Specified]**|**[FDStrengthThreshold]** で指定したしきい値を使用します。 機能依存の強さは、このしきい値より大きい場合にのみ報告されます。|  
|**[Exact]**|しきい値を指定しません。 機能依存の強さは、選択した列間の機能依存が完全に一致する場合にのみ報告されます。|  
  
 **[FDStrengthThreshold]**  
 0 ～ 1 の値を使用して、機能依存の強さが報告されるしきい値を指定します。 このプロパティの既定値は 0.95 です。 このオプションは、 **[ThresholdSetting]** で **[Specified]** が選択されている場合にのみ有効です。  
  
 **[MaxNumberOfViolations]**  
 出力で報告する機能依存違反の最大数を指定します。 このプロパティの既定値は 100 です。 **[ThresholdSetting]** で **[Exact]** が選択されている場合、このオプションは無効です。  
  
## <a name="see-also"></a>関連項目  
 [データ プロファイル タスク エディター ([全般] ページ)](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [単一テーブル クイック プロファイル フォーム &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
