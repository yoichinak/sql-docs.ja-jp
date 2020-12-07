---
description: SELECT DISTINCT FROM &lt; model &gt; (DMX)
title: SELECT DISTINCT FROM &lt; model &gt; (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: caefcdc2e081c0e8d0e7bee329d4dc5d4d5cfa22
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727653"
---
# <a name="select-distinct-from-ltmodel-gt-dmx"></a>SELECT DISTINCT FROM &lt; model &gt; (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  モデル内の選択された列に対して可能なすべての状態を返します。 返される値は、指定された列に不連続値、分離された数値、または連続する数値が含まれているかどうかによって異なります。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] DISTINCT [TOP <n>] <expression list> FROM <model>   
[WHERE <condition list>][ORDER BY <expression>]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 省略可能。 返す行数を指定する整数。  
  
 *式の一覧*  
 関連する列識別子 (モデルから派生したもの) または式のコンマ区切りのリスト。  
  
 *model*  
 モデル識別子。  
  
 *条件一覧*  
 列リストから返される値を制限する条件。  
  
 *式 (expression)*  
 省略可能。 スカラー値を返す式。  
  
## <a name="remarks"></a>解説  
 **SELECT DISTINCT FROM**ステートメントは、1つの列、または関連する列のセットでのみ機能します。 この句は、関連しない列のセットでは動作しません。  
  
 **SELECT DISTINCT FROM**ステートメントを使用すると、入れ子になったテーブル内の列を直接参照できます。 次に例を示します。  
  
```  
<model>.<table column reference>.<column reference>  
```  
  
 **SELECT DISTINCT FROM \<model> **ステートメントの結果は、列の種類によって異なります。 次の表は、サポートされている列の型およびステートメントからの出力について示しています。  
  
|列の型|Output|  
|-----------------|------------|  
|離散|列内の一意の値。|  
|Discretized|列内の分離された各バケットの中間点。|  
|継続的|列内の値の中間点。|  
  
## <a name="discrete-column-example"></a>不連続列の例  
 次のコードサンプルは、「 `[TM Decision Tree]` [基本的なデータマイニングチュートリアル](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))」で作成したモデルに基づいています。 このクエリでは、不連続列に存在する一意の値が返され `Gender` ます。  
  
```  
SELECT DISTINCT [Gender]  
FROM [TM Decision Tree]  
```  
  
 結果の例:  
  
|性別|  
|------------|  
||  
|F|  
|M|  
  
 不連続値を含む列の場合、結果には常に Missing 状態が含まれ、null 値として表示されます。  
  
## <a name="continuous-column-example"></a>連続列の例  
 次のコードサンプルでは、列のすべての値について、中間点、最小年齢、および最大有効期間が返されます。  
  
```  
SELECT DISTINCT [Age] AS [Midpoint Age],   
    RangeMin([Age]) AS [Minimum Age],   
    RangeMax([Age]) AS [Maximum Age]  
FROM [TM Decision Tree]  
```  
  
 結果の例:  
  
|Midpoint Age|Minimum Age|最大有効期間|  
|------------------|-----------------|-----------------|  
||||  
|62|26|97|  
  
 また、このクエリでは、欠損値を表すために null 値の単一行が返されます。  
  
## <a name="discretized-column-example"></a>離散化列の例  
 次のコード サンプルは、列 `Yearly Income]` のアルゴリズムで作成された各バケットの中間点、最大値、および最小値を返します。 この例の結果を再現するには、と同じ新しいマイニング構造を作成する必要があり `[Targeted Mailing]` ます。 ウィザードで、列のコンテンツの種類を [ `Yearly Income` **連続** ] から [ **分離**] に変更します。  
  
> [!NOTE]  
>  また、「基本的なマイニングチュートリアル」で作成したマイニングモデルを変更して、マイニング構造列を分離することもでき `Yearly Income]` ます。 この方法の詳細については、「 [マイニングモデルの列の分離を変更](/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model)する」を参照してください。 ただし、列の分離を変更した場合は、マイニング構造が強制的に再処理され、その構造を使用して作成した他のモデルの結果が変更されます。  
  
```  
SELECT DISTINCT [Yearly Income] AS [Bucket Average],   
    RangeMin([Yearly Income]) AS [Bucket Minimum],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
 結果の例:  
  
|バケット平均|Bucket Minimum|Bucket Maximum|  
|--------------------|--------------------|--------------------|  
||||  
|24610.7|10000|39221.41|  
|55115.73|39221.41|71010.05|  
|84821.54|71010.05|98633.04|  
|111633.9|98633.04|124634.7|  
|147317.4|124634.7|17万|  
  
 [年収] 列の値が5つのバケットに分離され、欠損値を表す null 値の行が追加されていることがわかります。  
  
 結果の小数点以下表示桁数は、クエリに使用するクライアントによって異なります。 ここでは、わかりやすくし、に表示される値を反映するために、小数点以下2桁に丸められてい [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ます。  
  
 たとえば、デシジョン ツリー ビューアーを使用してモデルを参照し、収入ごとにグループ化された顧客を含むノードをクリックすると、次のノードのプロパティがツールヒントに表示されます。  
  
 Age >= 69 と年収 < 39221.41  
  
> [!NOTE]  
>  最小バケットの最小値および最大バケットの最大値は、計測された値のうちの最大値と最小値になります。 この観測範囲外の値は、最小バケットと最大バケットに属していると見なされます。  
  
## <a name="see-also"></a>参照  
 [DMX&#41;を選択 &#40;](../dmx/select-dmx.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
