---
description: MDX 関数リファレンス (MDX)
title: MDX 関数リファレンス (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4d7590bf0fb76d9443ea9ceaebe2d8e2d00fbf57
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429794"
---
# <a name="mdx-function-reference-mdx"></a>MDX 関数リファレンス (MDX)


  Analysis Services には、多次元式 (MDX) 構文で関数を使用するためのが用意されています。 関数は、任意の有効な MDX ステートメントで使用できます。また、クエリ、カスタムロールアップ定義、およびその他の計算でよく使用されます。 ここでは、MDX 関数について説明します。  
  
 以下の表では、戻り値の種類ごとに関数がまとめられています。また、目次には、関数名がアルファベット順に一覧表示されます。  
  
## <a name="array-functions"></a>配列関数  
  
|機能|説明|  
|--------------|-----------------|  
|[SetToArray &#40;MDX&#41;](../mdx/settoarray-mdx.md)|1つ以上のセットを、ユーザー定義関数で使用する配列に変換します。|  
  
## <a name="hierarchy-functions"></a>階層関数  
  
|機能|説明|  
|--------------|-----------------|  
|[階層 &#40;MDX&#41;](../mdx/hierarchy-mdx.md)|指定されたメンバーまたはレベルを含む階層を返します。|  
|[ディメンション &#40;MDX&#41;](../mdx/dimension-mdx.md)|指定されたメンバー、レベル、または階層を含むディメンションを返します。|  
|[MDX&#41;&#40;ディメンション ](../mdx/dimensions-mdx.md)|数値または文字列式で指定された階層を返します。|  
  
## <a name="level-functions"></a>レベル関数  
  
|機能|説明|  
|--------------|-----------------|  
|[MDX&#41;&#40;レベル ](../mdx/level-mdx.md)|メンバーのレベルを返します。|  
|[MDX&#41;&#40;レベル ](../mdx/levels-mdx.md)|ディメンションまたは階層内の位置が数値式で指定されているか、文字列式で指定された名前を持つレベルを返します。|  
  
## <a name="logical-functions"></a>論理関数  
  
|機能|説明|  
|--------------|-----------------|  
|[IsAncestor &#40;MDX&#41;](../mdx/isancestor-mdx.md)|指定されたメンバーが別の指定されたメンバーの先祖であるかどうかを示す値を返します。|  
|[IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)|評価した式が空のセル値かどうかを返します。|  
|[IsGeneration &#40;MDX&#41;](../mdx/isgeneration-mdx.md)|指定したメンバーが指定したジェネレーションに存在するかどうかを返します。|  
|[IsLeaf &#40;MDX&#41;](../mdx/isleaf-mdx.md)|指定されたメンバーがリーフメンバーであるかどうかを返します。|  
|[IsSibling &#40;MDX&#41;](../mdx/issibling-mdx.md)|指定されたメンバーが別の指定されたメンバーの兄弟であるかどうかを示す値を返します。|  
  
## <a name="member-functions"></a>メンバー関数  
  
|機能|説明|  
|--------------|-----------------|  
|[先祖 &#40;MDX&#41;](../mdx/ancestor-mdx.md)|メンバーの先祖のうち、指定されたレベルまたは距離にある先祖を返します。|  
|[&#40;MDX&#41;の ClosingPeriod ](../mdx/closingperiod-mdx.md)|指定したレベルのメンバーの子孫のうち、最後の兄弟を返します。|  
|[いとこ &#40;MDX&#41;](../mdx/cousin-mdx.md)|親メンバーの下で、指定した子メンバーと同じ相対位置にある子メンバーを返します。|  
|[CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md)|反復処理中に、指定したディメンションまたは階層に沿って現在のメンバーを返します。|  
|[DataMember &#40;MDX&#41;](../mdx/datamember-mdx.md)|ディメンションの非リーフメンバーに関連付けられているシステムによって生成されたデータメンバーを返します。|  
|[DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)|ディメンションまたは階層の既定のメンバーを返します。|  
|[FirstChild &#40;MDX&#41;](../mdx/firstchild-mdx.md)|メンバーの先頭の子メンバーを返します。|  
|[FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)|メンバーの親の最初の子を返します。|  
|[項目 &#40;メンバー&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)|指定された組からメンバーを返します。|  
|[Lag &#40;MDX&#41;](../mdx/lag-mdx.md)|メンバーのディメンションの指定されたメンバーの前に指定された位置の数であるメンバーを返します。|  
|[LastChild &#40;MDX&#41;](../mdx/lastchild-mdx.md)|指定されたメンバーの最後の子を返します。|  
|[LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)|指定されたメンバーの親の最後の子を返します。|  
|[MDX&#41;&#40;潜在顧客 ](../mdx/lead-mdx.md)|ディメンション内の指定されたメンバーから指定された数だけ後にあるメンバーを返します。|  
|[LinkMember &#40;MDX&#41;](../mdx/linkmember-mdx.md)|指定された階層の指定されたメンバーと等価のメンバーを返します。|  
|[MDX&#41;&#41; &#40;のメンバー &#40;文字列 ](../mdx/members-string-mdx.md)|文字列式で指定されたメンバーを返します。|  
|[NextMember &#40;MDX&#41;](../mdx/nextmember-mdx.md)|指定されたメンバーを含むレベルの次のメンバーを返します。|  
|[OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)|指定されたレベルの子孫の中で最初の兄弟を返します。オプションで、指定したメンバーでも取得できます。|  
|[&#40;MDX&#41;の ParallelPeriod ](../mdx/parallelperiod-mdx.md)|指定されたメンバーと同じ相対位置で、前の期間のメンバーを返します。|  
|[親 &#40;MDX&#41;](../mdx/parent-mdx.md)|メンバーの親メンバーを返します。|  
|[PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)|指定されたメンバーを含むレベルの前のメンバーを返します。|  
|[StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)|MDX 形式の文字列によって指定されたメンバーを返します。|  
|[UnknownMember &#40;MDX&#41;](../mdx/unknownmember-mdx.md)|レベルまたはメンバーに関連付けられている不明なメンバーを返します。|  
|[ValidMeasure &#40;MDX&#41;](../mdx/validmeasure-mdx.md)|適用できないディメンションをトップ レベルにすることにより、仮想キューブ内の有効なメジャーを返します。|  
  
## <a name="numeric-functions"></a>数値関数  
  
|機能|説明|  
|--------------|-----------------|  
|[Aggregate (MDX)](../mdx/aggregate-mdx.md)|指定されたセットの組に対してメジャーまたはオプションで指定された数値式を集計することによって計算されたスカラー値を返します。|  
|[平均 &#40;MDX&#41;](../mdx/avg-mdx.md)|指定されたセットに対して評価される、メジャーの平均値またはオプションの数値式の平均値を返します。|  
|[CalculationCurrentPass (MDX)](../mdx/calculationcurrentpass-mdx.md)|指定されたクエリコンテキストのキューブの現在の計算パスを返します。|  
|[CalculationPassValue (MDX)](../mdx/calculationpassvalue-mdx.md)|キューブの指定した計算パスに対して評価される MDX 式の値を返します。|  
|[CoalesceEmpty &#40;MDX&#41;](../mdx/coalesceempty-mdx.md)|空のセル値を数値または文字列に連結し、結合された値を返します。|  
|[MDX&#41;&#40;相関関係 ](../mdx/correlation-mdx.md)|セットに対して評価される2つの系列の相関係数を返します。|  
|[&#40;ディメンション&#41; &#40;MDX&#41;のカウント ](../mdx/count-dimension-mdx.md)|キューブ内のディメンション数を返します。|  
|[MDX&#41;&#41; &#40;&#40;階層レベルのカウント ](../mdx/count-hierarchy-levels-mdx.md)|ディメンションまたは階層内のレベル数を返します。|  
|[Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)|セット内のセルの数を返します。|  
|[MDX&#41;&#41; &#40;組 &#40;数 ](../mdx/count-tuple-mdx.md)|組の次元数を返します。|  
|[&#40;MDX&#41;の共変性 ](../mdx/covariance-mdx.md)|バイアスをかけた母集団の公式を使用して、セットに対して評価される2つの系列の母共分散を返します。|  
|[MDX&#41;&#40;Coバリエーション ](../mdx/covariancen-mdx.md)|バイアスをかけない母集団の公式を使用して、セットに対して評価される2つの系列のサンプル共分散を返します。|  
|[DistinctCount &#40;MDX&#41;](../mdx/distinctcount-mdx.md)|セット内の個別の空でないタプルの数を返します。|  
|[IIf &#40;MDX&#41;](../mdx/iif-mdx.md)|論理テストによって判別される 2 つの値の 1 つを返します。|  
|[LinRegIntercept &#40;MDX&#41;](../mdx/linregintercept-mdx.md)|セットの線形回帰を計算し、回帰直線の切片の値を返します (y = ax + b)。|  
|[LinRegPoint &#40;MDX&#41;](../mdx/linregpoint-mdx.md)|セットの線形回帰を計算し、回帰直線の *y* = ax + b の値を返します。|  
|[LinRegR2 &#40;MDX&#41;](../mdx/linregr2-mdx.md)|セットの線形回帰を計算し、決定係数 R2 を返します。|  
|[MDX&#41;&#40;LinRegSlope ](../mdx/linregslope-mdx.md)|セットの線形回帰を計算し、回帰直線の傾きの値を返します (y = ax + b)。|  
|[LinRegVariance &#40;MDX&#41;](../mdx/linregvariance-mdx.md)|セットの線形回帰を計算し、回帰直線 (y = ax + b) に関連付けられている変位を返します。|  
|[MDX&#41;&#40;LookupCube ](../mdx/lookupcube-mdx.md)|同じデータベース内で別に指定されたキューブに対して評価される MDX 式の値を返します。|  
|[MDX&#41;の最大 &#40;](../mdx/max-mdx.md)|セットに対して評価される数値式の最大値を返します。|  
|[MDX&#41;&#40;中央値 ](../mdx/median-mdx.md)|セットに対して評価される数値式の中央値を返します。|  
|[MDX&#41;の最小 &#40;](../mdx/min-mdx.md)|セットに対して評価される数値式の最小値を返します。|  
|[序数 &#40;MDX&#41;](../mdx/ordinal-mdx.md)|レベルに関連付けられた、0から始まる序数値を返します。|  
|[MDX&#41;の予測 &#40;](../mdx/predict-mdx.md)|データマイニングモデルに対して評価される数値式の値を返します。|  
|[MDX&#41;&#40;順位付け ](../mdx/rank-mdx.md)|指定されたセット内の指定された組の1から始まる順位を返します。|  
|[RollupChildren &#40;MDX&#41;](../mdx/rollupchildren-mdx.md)|指定された単項演算子を使用して、指定されたメンバーの子の値をロールアップすることによって生成される値を返します。|  
|[Stddev &#40;MDX&#41;](../mdx/stddev-mdx.md)|[Stdev &#40;MDX&#41;](../mdx/stdev-mdx.md)の別名。|  
|[StddevP &#40;MDX&#41;](../mdx/stddevp-mdx.md)|[StdevP &#40;MDX&#41;](../mdx/stdevp-mdx.md)のエイリアス。|  
|[Stdev &#40;MDX&#41;](../mdx/stdev-mdx.md)|バイアスをかけない母集団の公式を使用して、セットに対して評価される数値式のサンプル標準偏差を返します。|  
|[StdevP &#40;MDX&#41;](../mdx/stdevp-mdx.md)|バイアスをかけた母集団の公式を使用して、セットに対して評価される数値式の母標準偏差を返します。|  
|[StrToValue &#40;MDX&#41;](../mdx/strtovalue-mdx.md)|MDX 形式の文字列によって指定された値を返します。|  
|[MDX&#41;の合計 &#40;](../mdx/sum-mdx.md)|セットに対して評価される数値式の合計を返します。|  
|[MDX&#41;&#40;値 ](../mdx/value-mdx.md)|メジャーの値を返します。|  
|[Var &#40;MDX&#41;](../mdx/var-mdx.md)|バイアスをかけない母集団の公式を使用して、セットに対して評価される数値式のサンプル分散を返します。|  
|[MDX&#41;&#40;分散 ](../mdx/variance-mdx.md)|[MDX&#41;の Var &#40;](../mdx/var-mdx.md)の別名。|  
|[VarianceP &#40;MDX&#41;](../mdx/variancep-mdx.md)|[VarP &#40;MDX&#41;](../mdx/varp-mdx.md)の別名。|  
|[VarP &#40;MDX&#41;](../mdx/varp-mdx.md)|バイアスをかけた母集団の公式を使用して、セットに対して評価される数値式の母分散を返します。|  
  
## <a name="set-functions"></a>集合関数  
  
|機能|説明|  
|--------------|-----------------|  
|[AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)|計算されるメンバーを指定されたセットに追加することによって生成されるセットを返します。|  
|[AllMembers &#40;MDX&#41;](../mdx/allmembers-mdx.md)|指定されたディメンション、階層、またはレベルのすべてのメンバー (計算されるメンバーを含む) を含むセットを返します。|  
|[先祖 &#40;MDX&#41;](../mdx/ancestors-mdx.md)|メンバーの先祖のうち、指定されたレベルまたは距離にあるすべての先祖のセットを返します。|  
|[先祖 &#40;MDX&#41;](../mdx/ascendants-mdx.md)|指定されたメンバー自体も含めたメンバーの先祖のセットを返します。|  
|[MDX&#41;&#40;軸 ](../mdx/axis-mdx.md)|軸で定義されたセットを返します。|  
|[&#40;MDX&#41;の下端数 ](../mdx/bottomcount-mdx.md)|セットを昇順に並べ替え、値の小さい方から指定された数の組を返します。|  
|[MDX&#41;&#40;下の割合 ](../mdx/bottompercent-mdx.md)|セットを昇順に並べ替え、累積合計が指定した割合以上になるように、最小値を持つ組のセットを返します。|  
|[BottomSum &#40;MDX&#41;](../mdx/bottomsum-mdx.md)|セットを昇順で並べ替え、合計が指定された値以下になるように、値の小さい方から組のセットを作成して返します。|  
|[Children &#40;MDX&#41;](../mdx/children-mdx.md)|指定されたメンバーの子メンバーを返します。|  
|[Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)|1 つ以上のセットのクロス積を返します。|  
|[CurrentOrdinal &#40;MDX&#41;](../mdx/currentordinal-mdx.md)|反復処理中に、セット内の現在のイテレーション数を返します。|  
|[MDX&#41;&#40;子孫 ](../mdx/descendants-mdx.md)|メンバーの子孫のうち、指定したレベルまたは距離にある子孫のセットを返します。他のレベルの子孫を含めたり除外したりすることもできます。|  
|[Distinct &#40;MDX&#41;](../mdx/distinct-mdx.md)|指定されたセットから重複した組を削除して、セットを返します。|  
|[DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)|セットのメンバーを、セット内で表される最下位レベルの1レベル下にドリルダウンします。または、セット内で指定されたメンバーのレベルのうち、必要に応じてレベルを1つ下に表示します。|  
|[DrilldownLevelBottom &#40;MDX&#41;](../mdx/drilldownlevelbottom-mdx.md)|指定されたレベルで、セットの最下位メンバーを1レベル下にドリルダウンします。|  
|[DrilldownLevelTop &#40;MDX&#41;](../mdx/drilldownleveltop-mdx.md)|セットの最上位メンバーを、指定されたレベルで1レベル下にドリルダウンします。|  
|[ドリルダウンメンバー &#40;MDX&#41;](../mdx/drilldownmember-mdx.md)|2 番目に指定されたセット内に存在する、指定されたセットのメンバーをドリル ダウンします。 または、関数は組のセットをドリルダウンします。|  
|[MDX&#41;&#40;ドリルダウンメンバー下部 ](../mdx/drilldownmemberbottom-mdx.md)|2番目に指定したセット内に存在する、指定したセットのメンバーをドリルダウンします。結果セットは、指定した数のメンバーに制限されます。 または、この関数は組のセットにもドリルダウンします。|  
|[MDX&#41;&#40;ドリルダウンメンバートップ ](../mdx/drilldownmembertop-mdx.md)|2番目に指定したセット内に存在する、指定したセットのメンバーをドリルダウンします。結果セットは、指定した数のメンバーに制限されます。 または、この関数は組のセットをドリルダウンします。|  
|[MDX&#41;&#40;ドリルアップの上位レベル ](../mdx/drilluplevel-mdx.md)|セットのメンバーのうち、指定されたレベルの下位に属するメンバーをドリル アップします。|  
|[MDX&#41;&#40;のドリルスルーメンバー ](../mdx/drillupmember-mdx.md)|2 番目に指定したセットに存在するメンバーを指定したセットにドリル アップします。|  
|[Except &#40;MDX&#41;](../mdx/except-mdx-function.md)|2 つのセットの差異を検出します。重複部分を保持することも可能です。|  
|[MDX&#41;&#40;存在 ](../mdx/exists-mdx.md)|1つ以上の他のセットの1つ以上の組に存在する1つのセットのメンバーのセットを返します。|  
|[MDX&#41;を抽出 &#40;](../mdx/extract-mdx.md)|抽出されたディメンション要素から組のセットを返します。|  
|[Filter &#40;MDX&#41;](../mdx/filter-mdx.md)|検索条件に基づいて、指定されたセットをフィルター処理した結果のセットを返します。|  
|[MDX&#41;を生成 &#40;](../mdx/generate-mdx.md)|あるセットを別のセットの各メンバーに適用し、その結果セットを和集合で結合します。 または、この関数は、セットに対して文字列式を評価することによって作成された連結文字列を返します。|  
|[&#40;MDX&#41;の Head ](../mdx/head-mdx.md)|重複部分を保持したまま、セット内の最初に指定した数の要素を返します。|  
|[Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)|階層内のセットのメンバーを並べ替えます。|  
|[MDX&#41;&#40;Intersect ](../mdx/intersect-mdx.md)|2つの入力セットの積集合を返します。オプションで重複部分を保持します。|  
|[&#40;MDX&#41;の LastPeriods ](../mdx/lastperiods-mdx.md)|指定されたメンバーまでのメンバーのセットを返します。|  
|[メンバー &#40;設定&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)|ディメンション、レベル、または階層内のメンバーのセットを返します。|  
|[Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)|時間ディメンションの年 (Year) レベルという制約の中で、指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。先頭は最初の兄弟、末尾は指定されたメンバーになります。|  
|[NameToSet &#40;MDX&#41;](../mdx/nametoset-mdx.md)|MDX 形式の文字列によって指定されたメンバーを含むセットを返します。|  
|[NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)|1 つ以上のセットのクロス積を 1 つのセットとして返します。ただし、空の組と、ファクト テーブル データに関連付けられていない組は含まれません。|  
|[MDX&#41;&#40;順序 ](../mdx/order-mdx.md)|指定されたセットのメンバーを整列します。必要に応じて、階層を維持または分割します。|  
|[PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)|時間ディメンションで指定されているレベル内で、指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。先頭は最初の兄弟、末尾は指定されたメンバーになります。|  
|[Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)|指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。最初の兄弟から始まり、指定されたメンバーで終わります。これは、時間ディメンションの *Quarter* レベルによって制限されます。|  
|[兄弟 &#40;MDX&#41;](../mdx/siblings-mdx.md)|指定されたメンバー自体を含めて、メンバーの兄弟を返します。|  
|[MDX&#41;の &#40;のメンバー ](../mdx/stripcalculatedmembers-mdx.md)|指定されたセットから計算されるメンバーを削除することによって生成されるセットを返します。|  
|[StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)|MDX 形式の文字列によって指定されたセットを返します。|  
|[サブセット &#40;MDX&#41;](../mdx/subset-mdx.md)|指定されたセットから組のサブセットを返します。|  
|[末尾 &#40;MDX&#41;](../mdx/tail-mdx.md)|セットの末尾からサブセットを返します。|  
|[ToggleDrillState &#40;MDX&#41;](../mdx/toggledrillstate-mdx.md)|メンバーのドリル状態を切り替えます。|  
|[TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)|セットを降順で並べ替え、最大値を持つ指定した数の要素を返します。|  
|[TopPercent &#40;MDX&#41;](../mdx/toppercent-mdx.md)|セットを降順で並べ替え、累積合計が指定された割合以下になるように、値の大きい方から組のセットを作成して返します。|  
|[TopSum &#40;MDX&#41;](../mdx/topsum-mdx.md)|セットを並べ替え、累積合計が少なくとも指定した値である最上位要素を返します。|  
|[Union &#40;MDX&#41;](../mdx/union-mdx.md)|2つのセットの和集合を返します。オプションで重複部分を保持します。|  
|[MDX&#41;&#40;順序を解除する ](../mdx/unorder-mdx.md)|指定したセットから適用される順序を削除します。|  
|[VisualTotals &#40;MDX&#41;](../mdx/visualtotals-mdx.md)|指定されたセット内の子メンバーを動的に合計することによって生成されるセットを返します。オプションで、結果のセルセット内の親メンバーの名前にパターンを使用できます。|  
|[Wtd &#40;MDX&#41;](../mdx/wtd-mdx.md)|時間ディメンションの週 (Week) レベルという制約の中で、指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。先頭は最初の兄弟、末尾は指定されたメンバーになります。|  
|[Ytd &#40;MDX&#41;](../mdx/ytd-mdx.md)|指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。最初の兄弟から始まり、指定されたメンバーで終わります。これは、時間ディメンションの *Year* レベルによって制限されます。|  
  
## <a name="string-functions"></a>文字列関数  
  
|機能|説明|  
|--------------|-----------------|  
|[CalculationPassValue (MDX)](../mdx/calculationpassvalue-mdx.md)|キューブの指定された計算パスを評価し、MDX 式の値を返します。|  
|[CoalesceEmpty &#40;MDX&#41;](../mdx/coalesceempty-mdx.md)|空のセル値を数値または文字列に連結し、結合された値を返します。|  
|[MDX&#41;を生成 &#40;](../mdx/generate-mdx.md)|あるセットを別のセットの各メンバーに適用し、その結果セットを和集合で結合します。 または、この関数は、セットに対して文字列式を評価することによって作成された連結文字列を返します。|  
|[IIf &#40;MDX&#41;](../mdx/iif-mdx.md)|論理テストによって判別される 2 つの値の 1 つを返します。|  
|[MDX&#41;&#40;LookupCube ](../mdx/lookupcube-mdx.md)|同じデータベース内で別に指定されたキューブに対して評価される MDX 式の値を返します。|  
|[MemberToStr &#40;MDX&#41;](../mdx/membertostr-mdx.md)|指定されたメンバーに対応する MDX 形式の文字列を返します。|  
|[MDX&#41;&#40;名前 ](../mdx/name-mdx.md)|ディメンション、階層、レベル、またはメンバーの名前を返します。|  
|[プロパティ &#40;MDX&#41;](../mdx/properties-mdx.md)|メンバー プロパティ値を含む文字列または厳密に型指定された値を返します。|  
|[SetToStr &#40;MDX&#41;](../mdx/settostr-mdx.md)|指定されたセットに対応する MDX 形式の文字列を返します。|  
|[TupleToStr &#40;MDX&#41;](../mdx/tupletostr-mdx.md)|指定された組に対応する MDX 形式の文字列を返します。|  
|[UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)|指定されたディメンション、階層、レベル、メンバーの一意の名前を返します。|  
|[ユーザー名 &#40;MDX&#41;](../mdx/username-mdx.md)|現在の接続のドメイン名とユーザー名を返します。|  
  
## <a name="subcube-functions"></a>サブキューブ関数  
  
|機能|説明|  
|--------------|-----------------|  
|[This (MDX)](../mdx/this-mdx.md)|現在のサブキューブを返します。|  
|[&#40;MDX&#41;を残します ](../mdx/leaves-mdx.md)|指定されたディメンション、メンバー、または組のリーフメンバーのセットを返します。|  
  
## <a name="tuple-functions"></a>組関数  
  
|機能|説明|  
|--------------|-----------------|  
|[現在の &#40;MDX&#41;](../mdx/current-mdx.md)|反復処理中に、セットから現在の組を返します。|  
|[項目 &#40;組&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)|セットから組を返します。|  
|[ルート &#40;MDX&#41;](../mdx/root-mdx.md)|キューブ、ディメンション、または組内の各属性階層の **すべて** のメンバーで構成される組を返します。|  
|[StrToTuple &#40;MDX&#41;](../mdx/strtotuple-mdx.md)|MDX 形式の文字列によって指定された組を返します。|  
  
## <a name="other-functions"></a>その他の関数  
  
|機能|説明|  
|--------------|-----------------|  
|[MDX&#41;&#40;エラー ](../mdx/error-mdx.md)|指定されたエラーメッセージを提供して、オプションでエラーを生成します。|  
  
## <a name="see-also"></a>参照  
 [MDX 言語リファレンス &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
