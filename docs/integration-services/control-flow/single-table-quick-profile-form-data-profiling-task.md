---
description: '[単一テーブル クイック プロファイル フォーム] (データ プロファイル タスク)'
title: '[単一テーブル クイック プロファイル フォーム] (データ プロファイル タスク) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.quickprofile.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: d2fac9ce-730e-474e-961a-69406b633778
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b974db6df0f18a8063201f9e83ec905b87267301
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495962"
---
# <a name="single-table-quick-profile-form-data-profiling-task"></a>[単一テーブル クイック プロファイル フォーム] (データ プロファイル タスク)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **[単一テーブル クイック プロファイル フォーム]** を使用すると、既定の設定を使用して単一のテーブルまたはビューをプロファイルするように、データ プロファイル タスクをすばやく構成できます。  
  
 データ プロファイル タスクの使用方法の詳細については、「 [データ プロファイル タスクのセットアップ](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)」を参照してください。 Data Profile Viewer を使用してデータ プロファイル タスクの出力を分析する方法の詳細については、「 [Data Profile Viewer](../../integration-services/control-flow/data-profile-viewer.md)」を参照してください。  
  
## <a name="options"></a>Options  
 **接続**  
 プロファイル対象のテーブルまたはビューを含む [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データベースに接続するには、.NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) を使用する既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続マネージャーを選択します。  
  
 **[テーブルまたはビュー]**  
 選択した接続マネージャーの接続先となる、データベース内の既存のテーブルまたはビューを選択します。  
  
 **Compute**  
 計算するプロファイルを選択します。  
  
|値|説明|  
|-----------|-----------------|  
|**列の NULL 比プロファイル**|選択したテーブルまたはビュー内のすべての該当する列に対して既定の設定を使用して、列の NULL 比プロファイルを計算します。<br /><br /> このプロファイルは、選択した列の NULL 値の比率を報告します。 このプロファイルを使用すると、列の NULL 値の比率が予想外に高いなどのデータの問題を特定できます。 このプロファイルの設定の詳細については、「[[列の NULL 比プロファイル要求] のオプション &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)」を参照してください。|  
|**列統計プロファイル**|選択したテーブルまたはビュー内のすべての該当する列に対して既定の設定を使用して、列統計プロファイルを計算します。<br /><br /> このプロファイルは、数値型列の最小値、最大値、平均値、標準偏差や、 **datetime** 列の最小値、最大値などの統計を報告します。 このプロファイルを使用すると、無効な日付などのデータの問題を特定できます。 このプロファイルの設定の詳細については、「[[列統計プロファイル要求] のオプション &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)」を参照してください。|  
|**列の値分布プロファイル**|選択したテーブルまたはビュー内のすべての該当する列に対して既定の設定を使用して、列の値分布プロファイルを計算します。<br /><br /> このプロファイルは、選択された列に含まれる値ごとに、その値と、テーブル内におけるその値の行の比率を報告します。 また、テーブル内の指定された比率を超えている行の値も報告できます。 このプロファイルを使用すると、列に含まれる個別の値の数が正しくないなどのデータの問題を特定できます。 このプロファイルの詳細については、「[[列の値分布プロファイル要求] のオプション &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)」を参照してください。|  
|**列長分布プロファイル**|選択したテーブルまたはビュー内のすべての該当する列に対して既定の設定を使用して、列長分布プロファイルを計算します。<br /><br /> このプロファイルは、選択された列に含まれる文字列値の長さごとに、その長さと、テーブル内におけるその長さの行の比率を報告します。 このプロファイルを使用すると、無効な値などのデータの問題を特定できます。 このプロファイルの設定の詳細については、「[[列長分布プロファイル要求] のオプション &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)」を参照してください。|  
|**列パターン プロファイル (Column Pattern Profile)**|選択したテーブルまたはビュー内のすべての該当する列に対して既定の設定を使用して、列パターン プロファイルを計算します。<br /><br /> このプロファイルは、文字列型の列に含まれる値に対応する一連の正規表現を報告します。 このプロファイルを使用すると、無効な文字列などのデータの問題を特定できます。 また、このプロファイルには、新しい値を検証するために将来使用できる正規表現も提示されます。 このプロファイルの設定の詳細については、「[[列パターン プロファイル要求] のオプション &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)」を参照してください。|  
|**候補キー プロファイル**|**[最大 N 個の列キー]** で指定された数までの列を含む列の組み合わせの候補キー プロファイルを計算します。<br /><br /> このプロファイルは、列または列のセットが、選択したテーブルのキーとして適しているかどうかを報告します。 また、このプロファイルを使用すると、キーとなる可能性がある列の重複値などのデータの問題を特定できます。 このプロファイルの設定の詳細については、「[[候補キー プロファイル要求] のオプション &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)」を参照してください。|  
|**[最大 N 個の列キー]**|テーブルまたはビューのキーとして考えられる組み合わせをテストする列の最大数を選択します。 既定値は 1 です。 最大値は 1000 です。 たとえば、3 を選択すると、1 つの列、2 つの列、および 3 つの列のキーの組み合わせがテストされます。|  
|**機能依存プロファイル**|**[決定列として最大 N 個の列]** で指定された数までの列を含む決定列の組み合わせの機能依存プロファイルを計算します。<br /><br /> このプロファイルは、ある列 (依存列) の値が別の列または列のセット (決定列) の値にどの程度依存しているかを報告します。 このプロファイルを使用すると、無効な値などのデータの問題を特定できます。 このプロファイルの設定の詳細については、「[[機能依存プロファイル要求] のオプション &#40;データ プロファイル タスク&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)」を参照してください。|  
|**[決定列として最大 N 個の列]**|決定列として考えられる組み合わせをテストする列の最大数を選択します。 既定値は 1 です。 最大値は 1000 です。 たとえば、2 を選択すると、単一の列または 2 つの列の組み合わせが別の (依存) 列の決定列である組み合わせがテストされます。|  
  
> [!NOTE]  
>   値包含プロファイル型は、 **[単一テーブル クイック プロファイル フォーム]** では使用できません。  
  
## <a name="see-also"></a>参照  
 [データ プロファイル タスク エディター ([全般] ページ)](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [データ プロファイル タスク エディター &#40;[プロファイル要求] ページ&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  
