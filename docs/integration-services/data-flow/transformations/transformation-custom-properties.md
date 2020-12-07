---
description: 変換のカスタム プロパティ
title: 変換のカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Slowly Changing Dimension transformation
- Import Column transformation [Integration Services]
- Sort transformation
- Unpivot transformation
- Merge Join transformation
- Data Mining Query transformation
- Fuzzy Grouping transformation
- Data Conversion transformation
- Fuzzy Lookup transformation
- Term Extraction transformation
- Row Count transformation custom properties [Integration Services]
- transformations [Integration Services], properties
- Pivot transformation
- Lookup transformation
- Percentage Sampling transformation
- Export Column transformation [Integration Services]
- Row Sampling transformation
- Conditional Split transformation custom properties [Integration Services]
- custom properties [Integration Services]
- Audit transformation
- Term Lookup transformation
- Script Component transformation custom properties [Integration Services]
- Derived Column transformation
- OLE DB Command transformation
- Copy Column transformation custom properties [Integration Services]
- Character Map transformation custom properties [Integration Services]
ms.assetid: 56f5df6a-56f6-43df-bca9-08476a3bd931
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ed5b4ad8fb62b326f48c85dced98fdb2686750c4
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194624"
---
# <a name="transformation-custom-properties"></a>変換のカスタム プロパティ

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、ほとんどのデータ フロー オブジェクトには共通するプロパティがありますが、それ以外にも、多くのデータ フロー オブジェクトにはオブジェクト固有のカスタム プロパティがあります。 カスタム プロパティにアクセスできるのは実行時のみで、このプロパティに関する説明は、『[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] マネージド プログラミング リファレンス マニュアル』には記載されていません。  
  
 ここでは、さまざまなデータ フローの変換のカスタム プロパティを一覧で示し、それぞれについて説明します。 データ フロー オブジェクトの大部分との共通プロパティについては、「 [Common Properties](../set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
 変換のプロパティの一部は、プロパティ式を使用して設定できます。 詳細については、「 [式を使って設定できるデータ フロー プロパティ](/previous-versions/sql/sql-server-2016/ms136104(v=sql.130))」をご覧ください。  
  
## <a name="transformations-with-custom-properties"></a>カスタム プロパティを持つ変換  

:::row:::
    :::column:::
        [集計](#aggregate)  
        [監査](#audit)  
        [キャッシュ変換](#cachetransform)  
        [文字マップ](#charmap)  
        [条件分割](#condsplit)  
        [列コピー](#copymap)  
        [データ変換](#dataconv)  
        [データ マイニング クエリ](#dmquery)  
        [[派生列]](#derived)  
    :::column-end:::
    :::column:::
        [列エクスポート](#extract)  
        [あいまいグループ化](#fgroup)  
        [あいまい参照](#flookup)  
        [列インポート](#insert)  
        [Lookup](#lookup)  
        [マージ結合](#mjoin)  
        [OLE DB コマンド](#oledbcmd)  
        [比率サンプリング](#percent)  
        [ピボット](#pivot)  
    :::column-end:::
    :::column:::
        [行数](#rowcount)  
        [行サンプリング](#rowsamp)  
        [スクリプト コンポーネント](#script)  
        [緩やかに変化するディメンション](#scd)  
        [Sort](#sort)  
        [用語抽出](#textract)  
        [用語参照](#tlookup)  
        [ピボット解除](#unpivot)  
    :::column-end:::
:::row-end:::

### <a name="transformations-without-custom-properties"></a>カスタム プロパティを持たない変換  
 コンポーネント、入力、出力といういずれのレベルでも、[マージ変換](../../../integration-services/data-flow/transformations/merge-transformation.md)、[マルチキャスト変換](../../../integration-services/data-flow/transformations/multicast-transformation.md)、[全体結合変換](../../../integration-services/data-flow/transformations/union-all-transformation.md)にはカスタム プロパティがありません。 これらの変換は、すべてのデータ フロー コンポーネントとの共通プロパティのみを使用します。  
  
##  <a name="aggregate-transformation-custom-properties"></a><a name="aggregate"></a> 集計変換のカスタム プロパティ  
 集計変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、集計変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|AutoExtendFactor|Integer|集計の際にメモリを拡張できる割合を 1 ～ 100% の範囲で指定する値。 このプロパティの既定値は **25**です。|  
|CountDistinctKeys|Integer|集計で書き込むことのできる個別カウントの正確な数を指定する値。 CountDistinctScale 値が指定されている場合、CountDistinctKeys の値が優先されます。|  
|CountDistinctScale|Integer (列挙)|集計でカウントできる、列の個別の値の概数を表す値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **Low** (1): キー値の数が最大 500,000 個であることを示します。<br /><br /> **Medium** (2): キー値の数が最大 5,000,000 個であることを示します。<br /><br /> **High** (3): キー値の数が 25,000,000 個以上であることを示します。<br /><br /> **Unspecified** (0): CountDistinctScale の値を使用しないことを示します。 **Unspecified** (0) オプションを使用すると、大規模なデータセットを処理する際のパフォーマンスに影響する場合があります。|  
|[キー]|Integer|集計で書き込まれる、GROUP BY キーの正確な数を指定する値。 KeyScalevalue が指定されている場合、Keys の値が優先されます。|  
|KeyScale|Integer (列挙)|集計で書き込むことができる、GROUP BY キーの概数を表す値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **Low** (1): キー値の数が最大 500,000 個であることを示します。<br /><br /> **Medium** (2): キー値の数が最大 5,000,000 個であることを示します。<br /><br /> **High** (3): キー値の数が 25,000,000 個以上であることを示します。<br /><br /> **Unspecified** (0): KeyScale の値が使用されないことを示します。|  
  
 次の表は、集計変換の出力のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|[キー]|Integer|集計で書き込むことができる、GROUP BY キーの正確な数を指定する値。 KeyScale の値が指定されている場合、Keys の値が優先されます。|  
|KeyScale|Integer (列挙)|集計で書き込むことができる、GROUP BY キーの概数を表す値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **Low** (1): キー値の数が最大 500,000 個であることを示します。<br /><br /> **Medium** (2): キー値の数が最大 5,000,000 個であることを示します。<br /><br /> **High** (3): キー値の数が 25,000,000 個以上であることを示します。<br /><br /> **Unspecified** (0): KeyScale の値が使用されないことを示します。|  
  
 次の表は、集計変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|AggregationColumnId|Integer|GROUP BY 関数または集計関数に含まれる列の **LineageID** 。|  
|AggregationComparisonFlags|Integer|集計変換が列の文字列データを比較する方法を指定する値。 詳しくは、「 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。|  
|AggregationType|Integer (列挙)|列に対して適用する集計操作を指定する値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **Group by** (0)<br /><br /> **Count** (1)<br /><br /> **Count all** (2)<br /><br /> **Countdistinct** (3)<br /><br /> **Sum** (4)<br /><br /> **Average** (5)<br /><br /> **Maximum** (7)<br /><br /> **Minimum** (6)|  
|CountDistinctKeys|Integer|集計の種類が **個別のカウント**の場合に、集計で書き込むことができるキーの正確な数を指定する値。 CountDistinctScale 値が指定されている場合、CountDistinctKeys の値が優先されます。|  
|CountDistinctScale|Integer (列挙)|集計の種類が **個別のカウント**の場合に、集計で書き込むことができるキーの概数を表す値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **Low** (1): キー値の数が最大 500,000 個であることを示します。<br /><br /> **Medium** (2): キー値の数が最大 5,000,000 個であることを示します。<br /><br /> **High** (3): キー値の数が 25,000,000 個以上であることを示します。<br /><br /> **Unspecified** (0): CountDistinctScale の値を使用しないことを示します。|  
|IsBig|Boolean|40 億より大きい値、または有効桁数が倍精度浮動小数点数より多い値が列に含まれるかどうかを示す値。 指定できる値は 0 または 1 です。 0 の場合、IsBig は **False** であり、列に大きな値または正確な値が含まれないことを示します。 このプロパティの既定値は 1 です。|  
  
 集計変換の入力および入力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Aggregate Transformation](../../../integration-services/data-flow/transformations/aggregate-transformation.md)」を参照してください。  
  
##  <a name="audit-transformation-custom-properties"></a><a name="audit"></a> 監査変換のカスタム プロパティ  
 コンポーネント レベルでは、監査変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
 次の表は、監査変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|LineageItemSelected|Integer (列挙)|出力用に選択された監査項目。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **実行インスタンスの GUID** (0)<br /><br /> **実行開始時刻** (4)<br /><br /> **コンピューター名** (5)<br /><br /> **パッケージ ID** (1)<br /><br /> **パッケージ名** (2)<br /><br /> **タスク ID** (8)<br /><br /> **タスク名** (7)<br /><br /> **ユーザー名** (6)<br /><br /> **バージョン ID** (3)|  
  
 監査変換の入力、入力列、および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [監査変換](../../../integration-services/data-flow/transformations/audit-transformation.md)」を参照してください。  
  
##  <a name="cache-transform-transformation-custom-properties"></a><a name="cachetransform"></a> キャッシュ変換のカスタム プロパティ  
 キャッシュ変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、キャッシュ変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|Connectionmanager|String|接続マネージャーの名前を指定します。|  
|[ValidateExternalMetadata]|Boolean|デザイン時に外部データ ソースを使用してキャッシュ変換を検証するかどうかを示します。 このプロパティが **False**に設定されている場合、外部データ ソースに対する検証は実行時に行われます。<br /><br /> 既定値は **True**です。|  
|AvailableInputColumns|String|使用できる入力列の一覧。|  
|InputColumns|String|選択した入力列の一覧。|  
|CacheColumnName|String|選択した入力列にマップする列の名前を指定します。<br /><br /> CacheColumnName プロパティの列の名前は、 **[キャッシュ接続マネージャー エディター]** の **[列]** ページに表示されている対応する列の名前に一致する必要があります。<br /><br /> 詳細については、「 [Cache Connection Manager Editor](../../connection-manager/cache-connection-manager.md)」をご覧ください。|  
  
##  <a name="character-map-transformation-custom-properties"></a><a name="charmap"></a> 文字マップ変換のカスタム プロパティ  
 コンポーネント レベルでは、文字マップ変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
 次の表は、文字マップ変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|出力列のソースである入力列の **LineageID** を指定する値。|  
|MapFlags|Integer (列挙)|文字マップ変換が列に対して行う文字列操作を指定する値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **バイトの反転** (2)<br /><br /> **全角** (6)<br /><br /> **半角** (5)<br /><br /> **ひらがな** (3)<br /><br /> **カタカナ** (4)<br /><br /> **言語の文字種** (7)<br /><br /> **小文字** (0)<br /><br /> **簡体中国語** (8)<br /><br /> **繁体字中国語**(9)<br /><br /> **大文字** (1)|  
  
 文字マップ変換の入力、入力列、および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md)」を参照してください。  
  
##  <a name="conditional-split-transformation-custom-properties"></a><a name="condsplit"></a> 条件分割変換のカスタム プロパティ  
 コンポーネント レベルでは、条件分割変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
 次の表は、条件分割変換の出力のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|EvaluationOrder|Integer|条件分割変換が評価する条件の一覧の中での、出力に関連付けられた条件の位置を指定する値。 条件は、最小値から最大値まで順に評価されます。|  
|式|String|条件分割変換が評価する条件を表す式。 列は系列 ID で示されます。|  
|FriendlyExpression|String|条件分割変換が評価する条件を表す式。 列はその名前で示されます。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。|  
|IsDefaultOut|Boolean|出力が既定の出力かどうかを示す値。|  
  
 条件分割変換の入力、入力列、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)」を参照してください。  
  
##  <a name="copy-column-transformation-custom-properties"></a><a name="copymap"></a> 列コピー変換のカスタム プロパティ  
 コンポーネント レベルでは、列コピー変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
 次の表は、列コピー変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|copyColumnId|Integer|この出力列のコピー元である入力列の **LineageID** 。|  
  
 列コピー変換の入力、入力列、および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Copy Column Transformation](../../../integration-services/data-flow/transformations/copy-column-transformation.md)」を参照してください。  
  
##  <a name="data-conversion-transformation-custom-properties"></a><a name="dataconv"></a> データ変換の変換のカスタム プロパティ  
 コンポーネント レベルでは、データ変換の変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
 次の表は、データ変換変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|FastParse|Boolean|列の解析に、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] が提供するロケール非依存型の高速な解析ルーチンを使用するか、またはロケール依存型の標準的な解析ルーチンを使用するかを示す値。 このプロパティの既定値は **False**です。 詳細については、「 [Fast Parse](../parsing-data.md) 」および「 [Standard Parse](../parsing-data.md)」を参照してください。 .<br /><br /> 注:このプロパティは、**データ変換変換エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|SourceInputColumnLineageId|Integer|出力列のソースである入力列の **LineageID** 。|  
  
 データ変換の変換の入力、入力列、および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)」を参照してください。  
  
##  <a name="data-mining-query-transformation-custom-properties"></a><a name="dmquery"></a> データ マイニング クエリ変換のカスタム プロパティ  
 データ マイニング クエリ変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、データ マイニング クエリ変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|接続オブジェクトの一意識別子。|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] プロジェクトまたは [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] データベースへの接続文字列。|  
|CatalogName|String|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] データベースの名前。|  
|ModelName|String|データ マイニング モデルの名前。|  
|ModelStructureName|String|マイニング構造の名前。|  
|ObjectRef|String|この変換が使用するデータ マイニング構造を指定する XML タグ。|  
|QueryText|String|この変換が使用する予測クエリ ステートメント。|  
  
 データ マイニング クエリ変換の入力、入力列、出力、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Data Mining Query Transformation](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)」を参照してください。  
  
##  <a name="derived-column-transformation-custom-properties"></a><a name="derived"></a> 派生列変換のカスタム プロパティ  
 コンポーネント レベルでは、派生列変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
 次の表は、派生列変換の入力列および出力列のカスタム プロパティを示しています。 派生列を新しい列として追加する場合、カスタム プロパティは新しい出力列に適用されます。既存の入力列の内容を派生結果で置き換える場合、カスタム プロパティは既存の入力列に適用されます。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|式|String|条件分割変換が評価する条件を表す式。 列は、その列の **LineageID** プロパティで示されます。|  
|FriendlyExpression|String|条件分割変換が評価する条件を表す式。 列はその名前で示されます。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。|  
  
 派生列変換の入力および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [派生列変換](../../../integration-services/data-flow/transformations/derived-column-transformation.md)」を参照してください。  
  
##  <a name="export-column-transformation-custom-properties"></a><a name="extract"></a> 列エクスポート変換のカスタム プロパティ  
 コンポーネント レベルでは、列エクスポート変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
 次の表は、列エクスポート変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|AllowAppend|Boolean|変換が既存のファイルにデータを追加するかどうかを指定する値。 このプロパティの既定値は **False**です。|  
|ForceTruncate|Boolean|データを書き込む前に、変換が既存のファイルのデータを切り捨てるかどうかを指定する値。 このプロパティの既定値は **False**です。|  
|FileDataColumnID|Integer|変換がファイルに挿入するデータを含む列を識別する値。 [列の抽出] の場合、このプロパティの値は **0**です。[ファイル パス列] の場合、このプロパティには [列の抽出] の **LineageID** が含まれます。|  
|WriteBOM|Boolean|バイト順マーク (BOM) をファイルに書き込むかどうかを指定する値。|  
  
 列エクスポート変換の入力、出力、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md)」を参照してください。  
  
##  <a name="import-column-transformation-custom-properties"></a><a name="insert"></a> 列インポート変換のカスタム プロパティ  
 コンポーネント レベルでは、列インポート変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
 次の表は、列インポート変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|ExpectBOM|Boolean|列インポート変換でバイト順マーク (BOM) を必要とするかどうかを指定する値。 BOM が必要になるのは、データが DT_NTEXT データ型の場合だけです。|  
|FileDataColumnID|Integer|変換がデータ フローに挿入するデータを含む列を識別する値。 挿入するデータを格納した列では、このプロパティ値は 0 です。ソース ファイルのパスが含まれる列では、このプロパティには、挿入するデータを格納した列の **LineageID** が含まれます。|  
  
 列インポート変換の入力、出力、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Import Column Transformation](../../../integration-services/data-flow/transformations/import-column-transformation.md)」を参照してください。  
  
##  <a name="fuzzy-grouping-transformation-custom-properties"></a><a name="fgroup"></a> あいまいグループ化変換のカスタム プロパティ  
 あいまいグループ化変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、あいまいグループ化変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|区切り記号|String|変換が使用するトークン区切り記号。 既定の区切り記号には以下の文字が含まれます。スペース ( )、コンマ (,)、ピリオド (.)、セミコロン (;)、コロン (:)、ハイフン (-)、二重引用符 (")、単一引用符 (')、アンパサンド (&)、スラッシュ (/)、円記号 (\\)、アット マーク (@)、感嘆符 (!)、疑問符 (?)、左かっこ (()、右かっこ ())、小なり (\<), greater than (>)、大なり (>)、左角かっこ ([)、右角かっこ (])、左中かっこ ({)、右中かっこ (})、パイプ文字 (&#124;)、シャープ記号 (#)、アスタリスク (*)、キャレット (^)、およびパーセント (%)。|  
|Exhaustive|Boolean|各入力レコードを、他のすべての入力レコードと比較するかどうかを指定する値。 値 **True** は、主としてデバッグ目的で設定されます。 このプロパティの既定値は **False**です。<br /><br /> 注:このプロパティは、**あいまいグループ化変換エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|MaxMemoryUsage|Integer|変換で使用される最大メモリ容量。 このプロパティの既定値は **0**で、動的なメモリの使用が許可されることを示します。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。<br /><br /> 注:このプロパティは、**あいまいグループ化変換エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|MinSimilarity|Double|重複部分を識別するために変換が使用する、類似性のしきい値。0 ～ 1 の間の値で表します。  このプロパティの既定値は 0.8 です。|  
  
 次の表は、あいまいグループ化変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|ExactFuzzy|Integer (列挙)|あいまい一致または完全一致のどちらを変換が実行するかを指定する値。 有効な値は **Exact** および **Fuzzy**です。 このプロパティの既定値は **Fuzzy**です。|  
|FuzzyComparisonFlags|Integer (列挙)|変換が列の文字列データを比較する方法を指定する値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **FullySensitive**<br /><br /> **IgnoreCase**<br /><br /> **IgnoreKanaType**<br /><br /> **IgnoreNonSpace**<br /><br /> **IgnoreSymbols**<br /><br /> **IgnoreWidth**<br /><br /> <br /><br /> 詳しくは、「 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。|  
|LeadingTrailingNumeralsSignificant|Integer (列挙)|数字の有意性を指定する値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **NumeralsNotSpecial** (0): 数字の意味を考慮しない場合に使用します。<br /><br /> **LeadingNumeralsSignificant** (1): 先頭の数字を考慮する場合に使用します。<br /><br /> **TrailingNumeralsSignificant** (2): 末尾の数字を考慮する場合に使用します。<br /><br /> **LeadingAndTrailingNumeralsSignificant** (3): 先頭および末尾の数字の両方を考慮する場合に使用します。|  
|MinSimilarity|Double|列の結合に使用される類似性のしきい値。0 ～ 1 の間の値で指定します。 しきい値より大きい行のみ、一致していると見なされます。|  
|ToBeCleaned|Boolean|重複部分を識別するためにこの列が使用されるかどうか、つまり、グループ化の対象となる列かどうかを指定する値。 このプロパティの既定値は **False**です。|  
  
 次の表は、あいまいグループ化変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|[列の型]|Integer (列挙)|出力列の型を識別する値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **Undefined** (0)<br /><br /> **KeyIn** (1)<br /><br /> **KeyOut** (2)<br /><br /> **Similarity** (3)<br /><br /> **ColumnSimilarity** (4)<br /><br /> **PassThru** (5)<br /><br /> **Canonical**(6)|  
|InputID|Integer|対応する入力列の **LineageID** 。|  
  
 あいまいグループ化変換の入力および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)」を参照してください。  
  
##  <a name="fuzzy-lookup-transformation-custom-properties"></a><a name="flookup"></a> あいまい参照変換のカスタム プロパティ  
 あいまい参照変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、あいまい参照変換のカスタム プロパティを示しています。 **ReferenceMetadataXML** 以外のすべてのプロパティは読み取り/書き込みです。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|CopyReferenceTable|Boolean|あいまい参照のインデックスの構築および以降の参照用に、参照テーブルのコピーを作成するかどうかを指定する値。 このプロパティの既定値は **True**です。|  
|区切り記号|String|列の値をトークンにする際に使用される区切り記号。 既定の区切り記号には以下の文字が含まれます。スペース ( )、コンマ (,)、ピリオド (.)、セミコロン (;)、コロン (:)、ハイフン (-)、二重引用符 (")、単一引用符 (')、アンパサンド (&)、スラッシュ (/)、円記号 (\\)、アット マーク (@)、感嘆符 (!)、疑問符 (?)、左かっこ (()、右かっこ ())、小なり (\<), greater than (>)、大なり (>)、左角かっこ ([)、右角かっこ (])、左中かっこ ({)、右中かっこ (})、パイプ文字 (&#124;)。 シャープ記号 (#)、アスタリスク (*)、キャレット (^)、およびパーセント (%)。|  
|DropExistingMatchIndex|Boolean|MatchIndexOptions の値が ReuseExistingIndex に設定されていない場合に、MatchIndexName で指定された一致インデックスを削除するかどうかを指定する値。 このプロパティの既定値は、 **True**です。|  
|Exhaustive|Boolean|各入力レコードを、他のすべての入力レコードと比較するかどうかを指定する値。 値 **True** は、主としてデバッグ目的で設定されます。 このプロパティの既定値は **False**です。<br /><br /> 注:このプロパティは、**あいまい参照変換エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|MatchIndexName|String|一致インデックスの名前。 一致インデックスは、変換が使用するインデックスを作成して保存するテーブルです。 一致インデックスが再使用される場合、MatchIndexName は再使用するインデックスを示します。 MatchIndexName は、有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別子名である必要があります。 たとえば、名前にスペースが含まれる場合は、角かっこで囲む必要があります。|  
|MatchIndexOptions|Integer (列挙)|変換が一致インデックスを管理する方法を指定する値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **ReuseExistingIndex** (0)<br /><br /> **GenerateNewIndex** (1)<br /><br /> **GenerateAndPersistNewIndex** (2)<br /><br /> **GenerateAndMaintainNewIndex** (3)|  
|MaxMemoryUsage|Integer|参照テーブルの最大キャッシュ サイズ。 このプロパティの既定値は **0**で、これはキャッシュ サイズが無制限であることを示します。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。<br /><br /> 注:このプロパティは、**あいまい参照変換エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|MaxOutputMatchesPerInput|Integer|変換で各入力行に対して返される一致結果の最大数。 このプロパティの既定値は **1**です。<br /><br /> 注:100 より大きい値は**詳細エディター**でのみ指定できます。|  
|MinSimilarity|Integer|変換がコンポーネント レベルで使用する類似性のしきい値。0 ～ 1 の間の値で指定します。 しきい値より大きい行のみ、一致していると見なされます。|  
|ReferenceMetadataXML|String|[!INCLUDE[ssInternalOnly](../../../includes/ssinternalonly-md.md)]|  
|ReferenceTableName|String|参照テーブルの名前。 名前は、有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別子名である必要があります。 たとえば、名前にスペースが含まれる場合は、角かっこで囲む必要があります。|  
|WarmCaches|Boolean|true の場合は、実行が開始される前に、インデックスおよび参照テーブルが、参照によって部分的にメモリに読み込まれます。 これにより、パフォーマンスが向上する可能性があります。|  
  
 次の表は、あいまい参照変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|FuzzyComparisonFlags|Integer|変換が列の文字列データを比較する方法を指定する値。 詳しくは、「 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。|  
|FuzzyComparisonFlagsEx|Integer (列挙)|どの拡張比較フラグを変換が使用するかを指定する値。 有効な値は **MapExpandLigatures**、 **MapFoldCZone**、 **MapFoldDigits**、 **MapPrecomposed**、および NoMapping です。 **NoMapping** は、他のフラグと組み合わせて使用することはできません。|  
|JoinToReferenceColumn|String|列と結合される参照テーブル内の列の名前を指定する値。|  
|JoinType|Integer|あいまい一致または完全一致のどちらを変換が実行するかを指定する値。 このプロパティの既定値は **Fuzzy**です。 完全結合型を表す整数値は **1** で、あいまい結合型を表す値は **2**です。|  
|MinSimilarity|Double|変換が列レベルで使用する類似性のしきい値。0 ～ 1 の間の値で指定します。 しきい値より大きい行のみ、一致していると見なされます。|  
  
 次の表は、あいまい参照変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
> [!NOTE]  
>  対応する入力列からのパススルー値を含む出力列の場合、CopyFromReferenceColumn は空で、SourceInputColumnLineageID には、対応する入力列の **LineageID** が含まれます。 参照結果を含む出力列の場合、CopyFromReferenceColumn には参照列の名前が含まれ、SourceInputColumnLineageID は空です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|[列の型]|Integer (列挙)|変換が出力に追加する列の、出力列の型を指定する値。 このプロパティの値は、次のいずれか 1 つです。<br /><br /> **Undefined** (0)<br /><br /> **Similarity** (1)<br /><br /> **Confidence** (2)<br /><br /> **ColumnSimilarity** (3)|  
|CopyFromReferenceColumn|String|参照テーブル内の列のうち、出力列の値を提供する列の名前を指定する値。|  
|SourceInputColumnLineageId|Integer|この出力列に値を提供する入力列を指定する値。|  
  
 あいまい参照変換の入力および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)」を参照してください。  
  
##  <a name="lookup-transformation-custom-properties"></a><a name="lookup"></a> 参照変換のカスタム プロパティ  
 参照変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、参照変換のカスタム プロパティを示しています。 **ReferenceMetadataXML** 以外のすべてのプロパティは読み取り/書き込みです。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|CacheType|Integer (列挙)|参照テーブルのキャッシュの種類。 値は、 **Full** (0)、 **Partial** (1)、 **None** (2) です。 このプロパティの既定値は **Full**です。|  
|DefaultCodePage|Integer|コード ページに関する情報をデータ ソースから取得できない場合に使用する既定のコード ページ。|  
|MaxMemoryUsage|Integer|参照テーブルの最大キャッシュ サイズ。 このプロパティの既定値は **25**で、これはキャッシュ サイズが無制限であることを示します。|  
|MaxMemoryUsage64|Integer|64 ビット コンピューター上での参照テーブルの最大キャッシュ サイズ。|  
|NoMatchBehavior|Integer (列挙)|参照データセットに一致するエントリがない行をエラーとして処理するかどうかを指定する値。<br /><br /> このプロパティが " **一致するエントリがない行をエラーとして処理します** " (0) に設定されている場合、一致するエントリがない行はエラーとして処理されます。 **[参照変換エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、この種類のエラーが発生した場合の処理方法を指定できます。 詳細については、「[[参照変換エディター] ([エラー出力] ページ)](./lookup-transformation.md)」をご覧ください。<br /><br /> このプロパティが " **一致するエントリがない行を不一致出力に送信します** " (1) に設定されている場合、行はエラーとして処理されません。<br /><br /> 既定値は " **一致するエントリがない行をエラーとして処理します** " (0) です。|  
|ParameterMap|String|**SqlCommand** ステートメント内で使用されるパラメーターにマップする系列 ID を、セミコロンで区切った一覧。|  
|ReferenceMetadataXML|String|参照テーブル内の列のうち、変換が出力にコピーする列のメタデータ。|  
|SqlCommand|String|参照テーブルを設定する SELECT ステートメント。|  
|SqlCommandParam|String|参照テーブルを設定するパラメーター化 SQL ステートメント。|  
  
 次の表は、参照変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|列のコピー元である、参照テーブル内の列の名前。|  
|JoinToReferenceColumns|String|参照元の列を結合させる、参照テーブル内の列の名前。|  
  
 次の表は、参照変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|列のコピー元である、参照テーブル内の列の名前。|  
  
 参照変換の入力および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
##  <a name="merge-join-transformation-custom-properties"></a><a name="mjoin"></a> マージ結合変換のカスタム プロパティ  
 マージ結合変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、マージ結合変換のカスタム プロパティを示しています。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|JoinType|Integer (列挙)|結合が、内部結合 (2)、左外部結合 (1)、または完全外部結合 (0) のいずれであるかを指定します。|  
|MaxBuffersPerInput|Integer|マイクロソフトが行った変更により、マージ結合変換によってメモリが過度に消費されるリスクが軽減したため、 **MaxBuffersPerInput** プロパティの値を構成する必要はなくなりました。 この問題は、マージ結合の複数の入力からデータが不均一なレートで生成される場合に発生することがありました。|  
|NumKeyColumns|Integer|結合で使用される列数。|  
|TreatNullsAsEqual|Boolean|変換が NULL 値を等しい値として処理するかどうかを指定する値。 このプロパティの既定値は **True**です。 プロパティの値が **False**の場合、変換は NULL 値を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と同じ方式で処理します。|  
  
 次の表は、マージ結合変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|InputColumnID|Integer|この出力列にデータがコピーされる入力列の **LineageID** 。|  
  
 マージ結合変換の入力、入力列、および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Merge Join Transformation](../../../integration-services/data-flow/transformations/merge-join-transformation.md)」を参照してください。  
  
##  <a name="ole-db-command-transformation-custom-properties"></a><a name="oledbcmd"></a> OLE DB コマンド変換のカスタム プロパティ  
 OLE DB コマンド変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、OLE DB コマンド変換のカスタム プロパティを示しています。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|CommandTimeOut|Integer|SQL コマンドがタイムアウトになるまでの最大秒数。この値に **0** を指定すると、時間は無制限になります。 このプロパティの既定値は **0**です。|  
|DefaultCodePage|Integer|コード ページに関する情報をデータ ソースから取得できない場合に使用するコード ページ。|  
|SqlCommand|String|データ フロー内の各行に対して変換が実行する Transact-SQL ステートメント。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。|  
  
 次の表は、OLE DB コマンド変換の外部列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|DBParamInfoFlag|Integer (ビット マスク)|パラメーター特性を説明するフラグのセット。 詳細については、MSDN ライブラリの OLE DB に関するドキュメントで、DBPARAMFLAGSENUM のセクションを参照してください。|  
  
 OLE DB コマンド変換の入力、入力列、出力、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [OLE DB Command Transformation](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)」を参照してください。  
  
##  <a name="percentage-sampling-transformation-custom-properties"></a><a name="percent"></a> 比率サンプリング変換のカスタム プロパティ  
 比率サンプリング変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、比率サンプリング変換のカスタム プロパティを示しています。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|乱数ジェネレーターが使用するシード値。 このプロパティの既定値は **0**で、これは変換がティック数を使用することを示します。|  
|SamplingValue|Integer|サンプリングするサイズを、ソースに対するパーセントで示した値。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。|  
  
 次の表は、比率サンプリング変換の出力のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|Selected|Boolean|サンプリングされた行を送る出力を指定します。 選択された出力では Selected は **True**に設定され、選択されていない出力では Selected は **False**に設定されます。|  
  
 比率サンプリング変換の入力、入力列、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)」を参照してください。  
  
##  <a name="pivot-transformation-custom-properties"></a><a name="pivot"></a> ピボット変換のカスタム プロパティ  
 次の表は、ピボット変換のカスタム コンポーネントのプロパティを示しています。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|**PassThroughUnmatchedPivotKeyts**|Boolean|パッケージが実行されるときに、[ピボット キー] 列に不明な値が含まれている行を無視して、ピボット キーの値をすべてログ メッセージに出力するようにピボット変換を構成する場合は、 **True** に設定します。|  
  
 次の表は、ピボット変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|PivotUsage|Integer (列挙)|データセットがピボットされるときの、列の役割を指定する値。<br /><br /> **0**:<br />                      列はピボットされず、列の値は変換出力に渡されます。<br /><br /> **1**:<br />                      列は、1 つ以上の行を 1 つのセットの部分として識別するための設定キーとなります。 同じ設定キーを持つすべての入力行が、1 つの出力行に結合されます。<br /><br /> **2**:<br />                      列はピボット列となります。 各列の値から、少なくとも 1 つの列が作成されます。<br /><br /> **3**:<br />                      この列の値は、ピボットの結果として作成された列に配置されます。|  
  
 次の表は、ピボット変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|PivotKeyValue|String|PivotUsage プロパティの値によってピボット キーとしてマークされた列に設定できる値のうちの 1 つ。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。|  
|SourceColumn|Integer|ピボットされた値または -1 を含む入力列の **LineageID** 。 この値に -1 を指定すると、ピボット操作でその列が使用されないことを示します。|  
  
 詳細については、「 [Pivot Transformation](../../../integration-services/data-flow/transformations/pivot-transformation.md)」を参照してください。  
  
##  <a name="row-count-transformation-custom-properties"></a><a name="rowcount"></a> 行数変換のカスタム プロパティ  
 行数変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、行数変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|VariableName|String|行数を保持する変数の名前。|  
  
 行数変換の入力、入力列、出力、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md)」を参照してください。  
  
##  <a name="row-sampling-transformation-custom-properties"></a><a name="rowsamp"></a> 行サンプリング変換のカスタム プロパティ  
 行サンプリング変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、行サンプリング変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|乱数ジェネレーターが使用するシード値。 このプロパティの既定値は **0**で、これは変換がティック数を使用することを示します。|  
|SamplingValue|Integer|サンプルの行数。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。|  
  
 次の表は、行サンプリング変換の出力のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|Selected|Boolean|サンプリングされた行を送る出力を指定します。 選択された出力では Selected は **True**に設定され、選択されていない出力では Selected は **False**に設定されます。|  
  
 次の表は、行サンプリング変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|出力列のソースである入力列の **LineageID** を指定する値。|  
  
 行サンプリング変換の入力および入力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)」を参照してください。  
  
##  <a name="script-component-custom-properties"></a><a name="script"></a> スクリプト コンポーネントのカスタム プロパティ  
 スクリプト コンポーネントには、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。 スクリプト コンポーネントの機能が変換元、変換、または変換先のいずれの場合でも、同じカスタム プロパティを使用できます。  
  
 次の表は、スクリプト コンポーネントのカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|[ReadOnlyVariables]|String|スクリプト コンポーネントが読み取り専用でアクセスできる変数の、コンマ区切りの一覧。|  
|[ReadWriteVariables]|String|スクリプト コンポーネントが読み取り/書き込みアクセスできる変数の、コンマ区切りの一覧。|  
  
 スクリプトの開発者がカスタム プロパティを作成しない限り、スクリプト コンポーネントの入力、入力列、出力、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Script Component](../../../integration-services/data-flow/transformations/script-component.md)」を参照してください。  
  
##  <a name="slowly-changing-dimension-transformation-custom-properties"></a><a name="scd"></a> 緩やかに変化するディメンション変換のカスタム プロパティ  
 緩やかに変化するディメンション変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、緩やかに変化するディメンション変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|CurrentRowWhere|String|同じビジネス キーが設定された行から現在の行を選択する SELECT ステートメントの WHERE 句。|  
|EnableInferredMember|Boolean|推論メンバー更新が検出されるかどうかを指定する値。 このプロパティの既定値は **True**です。|  
|FailOnFixedAttributeChange|Boolean|固定属性を持つ行の列に変更が含まれるとき、またはディメンション テーブル内の参照が失敗したときに、変換が失敗するかどうかを指定する値。 受信する行に新しいレコードが含まれることが期待される場合は、変換が失敗によって新しいレコードを識別するので、参照に失敗しても変換が継続されるよう、この値を **True** に設定します。 このプロパティの既定値は **False**です。|  
|FailOnLookupFailure|Boolean|既存のレコードの参照が失敗したときに、変換が失敗するかどうかを指定する値。 このプロパティの既定値は **False**です。|  
|IncomingRowChangeType|Integer|受信するすべての行が新しい行であるか、または変換が変更の種類を検出する必要があるかを指定する値。|  
|InferredMemberIndicator|String|推論メンバーの列名。|  
|SqlCommand|String|スキーマ行セットを作成するために使用される SQL ステートメント。|  
|UpdateChangingAttributeHistory|Boolean|履歴属性の更新を変換出力に送り、変化する属性を更新するかどうかを示す値。|  
  
 次の表は、緩やかに変化するディメンション変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|[列の型]|Integer (列挙)|列の更新の種類。 値は次のとおりです。**Changing Attribute** (2)、**Fixed Attribute** (4)、**Historical Attribute** (3)、**Key** (1)、**Other** (0)。|  
  
 緩やかに変化するディメンション変換の入力、出力、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)」を参照してください。  
  
##  <a name="sort-transformation-custom-properties"></a><a name="sort"></a> 並べ替え変換のカスタム プロパティ  
 並べ替え変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、並べ替え変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|EliminateDuplicates|Boolean|重複した行を変換出力から削除するかどうかを指定する値。 このプロパティの既定値は **False**です。|  
|MaximumThreads|Integer|変換が並べ替えに使用できるスレッドの最大数。 この値に **0** を指定すると、スレッド数が無制限になります。 このプロパティの既定値は **0**です。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。|  
  
 次の表は、並べ替え変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|NewComparisonFlags|Integer (ビット マスク)|変換が列の文字列データを比較する方法を指定する値。 詳しくは、「 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。|  
|NewSortKeyPosition|Integer|列の並べ替え順序を指定する値。 この値に 0 を指定すると、データはこの列を基準にして並べ替えされません。|  
  
 次の表は、並べ替え変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|SortColumnID|Integer|並べ替え列の **LineageID** 。|  
  
 並べ替え変換の入力および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Sort Transformation](../../../integration-services/data-flow/transformations/sort-transformation.md)」を参照してください。  
  
##  <a name="term-extraction-transformation-custom-properties"></a><a name="textract"></a> 用語抽出変換のカスタム プロパティ  
 用語抽出変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、用語抽出変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|--------------|-----------------|  
|FrequencyThreshold|Integer|ある用語が何回以上出現したら抽出するかを示す数値。 このプロパティの既定値は **2**です。|  
|IsCaseSensitive|Boolean|名詞や名詞句を抽出する際、大文字と小文字を区別するかどうかを指定する値。 このプロパティの既定値は **False**です。|  
|MaxLengthOfTerm|Integer|用語の最大長を表す数値。 このプロパティは、句に対してのみ適用されます。 このプロパティの既定値は **12**です。|  
|NeedRefenceData|Boolean|参照テーブル内に格納された除外用語の一覧を使用するかどうかを指定する値。 このプロパティの既定値は **False**です。|  
|OutTermColumn|String|除外用語を含む列の名前。|  
|OutTermTable|String|除外用語を格納した列が含まれるテーブルの名前。|  
|ScoreType|Integer|用語に関連付けられているスコアの種類を指定する値。 有効な値は、頻度を示す 0 と、TFIDF スコアを示す 1 です。 TFIDF スコアは、Term Frequency と Inverse Document Frequency の積であり、次のように定義されます: 用語 T の TFIDF = (T の頻度) \* log( (入力の行数) / (T を含む行数) ) として定義されます。 このプロパティの既定値は **0**です。|  
|WordOrPhrase|Integer|用語の種類を指定する値。 有効な値は、単語のみを示す 0、名詞句のみを示す 1、および単語と名詞句の両方を示す 2 です。 このプロパティの既定値は **0**です。|  
  
 用語抽出変換の入力、入力列、出力、および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)」を参照してください。  
  
##  <a name="term-lookup-transformation-custom-properties"></a><a name="tlookup"></a> 用語参照変換のカスタム プロパティ  
 用語参照変換には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、用語参照変換のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|IsCaseSensitive|Boolean|入力列のテキストと参照用語との比較で、大文字と小文字を区別するかどうかを指定する値。 このプロパティの既定値は **False**です。|  
|RefTermColumn|String|参照用語を含む列の名前。|  
|RefTermTable|String|参照用語を格納した列が含まれるテーブルの名前。|  
  
 次の表は、用語参照変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|InputColumnType|Integer|列の使用方法を指定する値。 有効な値は、パススルー列を示す 0、参照列を示す 1、パススルー列と参照列の両方である列を示す 2 です。|  
  
 次の表は、用語参照変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|CustomLineageID|Integer|入力列の **LineageID** が 0 または 2 の場合、対応する入力列の **InputColumnType** 。|  
  
 用語参照変換の入力および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)」を参照してください。  
  
##  <a name="unpivot-transformation-custom-properties"></a><a name="unpivot"></a> ピボット解除変換のカスタム プロパティ  
 コンポーネント レベルでは、ピボット解除変換はすべてのデータ フロー コンポーネントとの共通プロパティのみを持ちます。  
  
> [!NOTE]  
>  このセクションでは、「 [ピボット解除変換](../../../integration-services/data-flow/transformations/unpivot-transformation.md) 」に示されているピボット解除の例に基づいて、ここで示したオプションの使用方法を説明します。  
  
 次の表は、ピボット解除変換の入力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|DestinationColumn|Integer|入力列をマップする出力列の **LineageID** 。 この値を -1 に設定すると、入力列が出力列にマップされないことを示します。|  
|PivotKeyValue|String|変換の出力列にコピーされる値。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。<br /><br /> 「 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)」で説明しているピボット解除の例では、ピボット値は Ham、Coke、Milk、Beer、および Chips というテキスト値です。 これらの値は、 **Pivot Key Value Column Name** オプションによって指定された新しい列 Product で、テキスト値として表示されます。|  
  
 次の表は、ピボット解除変換の出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|PivotKey|Boolean|入力列の **PivotKeyValue** プロパティの値を、この出力列に書き込むかどうかを示す値。<br /><br /> 「 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)」で説明している例では、ピボット値の列名は **Product** であり、この新しい列 **Product** に対して、Ham、Coke、Milk、Beer、Chips の各列がピボット解除されて格納されます。|  
  
 ピボット解除変換の入力および出力には、カスタム プロパティがありません。  
  
 詳細については、「 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [共通プロパティ](../set-the-properties-of-a-data-flow-component.md)   
 [パスのプロパティ](../integration-services-paths.md)   
 [式を使って設定できるデータ フロー プロパティ](/previous-versions/sql/sql-server-2016/ms136104(v=sql.130))  
  
