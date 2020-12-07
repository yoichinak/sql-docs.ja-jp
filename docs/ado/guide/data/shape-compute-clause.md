---
description: Shape COMPUTE 句
title: Shape COMPUTE 句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
author: rothja
ms.author: jroth
ms.openlocfilehash: 67411cf8d9be50571a515b5e7cf906fd19a650ec
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979603"
---
# <a name="shape-compute-clause"></a>Shape COMPUTE 句
Shape COMPUTE 句は、子**レコード**セットへの参照で構成される親**レコードセット**を生成します。チャプター、新しい、または計算列、または子**レコード**セットまたは以前にデザインされた**レコードセット**に対して集計関数を実行した結果の内容を含む、省略可能な列。また、オプションの BY 句に示されている子**レコードセット**のすべての列が表示されます。  
  
## <a name="syntax"></a>構文  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>説明  
 この句の部分は次のとおりです。  
  
 *child-command*  
 は、次のいずれかで構成されます。  
  
-   {}子**レコードセット**オブジェクトを返す中かっこ ("") 内のクエリコマンド。 コマンドは基になるデータプロバイダーに対して発行され、その構文はそのプロバイダーの要件によって異なります。 これは通常 SQL 言語ですが、ADO では特定のクエリ言語を必要としません。  
  
-   既存の形状が指定された **レコードセット**の名前。  
  
-   別の shape コマンド。  
  
-   テーブルキーワードと、その後にデータプロバイダーのテーブル名を指定します。  
  
 *子-エイリアス*  
 *子コマンド*によって返される**レコードセット**を参照するために使用される別名。 *子エイリアス*は、COMPUTE 句の列のリストに必要であり、親と子の**Recordset**オブジェクトの間のリレーションシップを定義します。  
  
 *追加された列リスト*  
 生成された親の列を各要素が定義するリスト。 各要素には、チャプター列、新しい列、計算列、または子 **レコードセット**の集計関数の結果として得られる値が含まれます。  
  
 *grp-フィールド一覧*  
 子で行をグループ化する方法を指定する親および子の **レコードセット** オブジェクトの列の一覧。  
  
 [ *Grp] ボックス* の各列には、子レコードセットオブジェクトと親 **レコードセット** オブジェクトに対応する列があります。 親 **レコードセット**の各行につい *ては、各列に* 一意の値が割り当てられています。また、親行によって参照される子 **レコードセット** は、親行と同じ値 *を持つ、* 子行だけで構成されます。  
  
 BY 句が含まれている場合、子 **レコードセット**の行は COMPUTE 句の列に基づいてグループ化されます。 親 **レコードセット** には、子 **レコードセット**内の行のグループごとに1つの行が含まれます。  
  
 BY 句を省略した場合、子 **レコードセット** 全体が1つのグループとして扱われ、親 **レコードセット** には1行だけが格納されます。 その行は、子 **レコードセット**全体を参照します。 BY 句を省略すると、子 **レコードセット**全体に対する "総計" 集計を計算できます。  
  
 次に例を示します。  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 親 **レコードセット** がどのように形成されているか (COMPUTE または using APPEND を使用) に関係なく、子レコード **セット**に関連付けられているチャプター列が含まれます。 必要に応じて、子行に対する集計 (SUM、MIN、MAX など) を含む列が親 **レコードセット** に含まれている場合もあります。 親と子の両方の **レコードセット** には、 **レコードセット**内の行に式を含む列と、新しい列と最初に空の列が含まれている場合があります。  
  
## <a name="operation"></a>操作  
 子 *コマンド* がプロバイダーに対して発行され、これによって子 **レコードセット**が返されます。  
  
 COMPUTE 句では、親 **レコードセット**の列を指定します。これには、子 **レコードセット**への参照、1つ以上の集計、計算式、または新しい列があります。 BY 句がある場合は、それによって定義される列も親 **レコードセット**に追加されます。 BY 句は、子 **レコードセット** の行をグループ化する方法を指定します。  
  
 たとえば、"人口統計" という名前のテーブルがあるとします。これは、州、市区町村、および人口の各フィールドで構成されます。 (テーブル内の母集団の数値は例としてのみ提供されています)。  
  
|State|City|[母集団]|  
|-----------|----------|----------------|  
|WA|Seattle|70万|  
|OR|Medford|200,000|  
|OR|Portland|400,000|  
|CA|Los Angeles|80万|  
|CA|San Diego|60万|  
|WA|Tacoma|500,000|  
|OR|Corvallis|300,000|  
  
 ここで、次の shape コマンドを発行します。  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 このコマンドは、2つのレベルを持つ、形状がある **レコードセット** を開きます。 親レベルは、集計列**Recordset** ( `SUM(rs.population)` )、子**レコードセット**を参照する列 ( `rs` )、および子**レコードセット**をグループ化するための列 () を使用して生成されたレコードセットです `state` 。 子レベルは、クエリコマンドによって返される **レコードセット** です ( `select * from demographics` )。  
  
 子 **レコードセット** の詳細行は状態ごとにグループ化されますが、それ以外の場合は特定の順序でグループ化されません。 つまり、グループはアルファベット順または数字順にはなりません。 **親レコードセットを**並べ替える場合は、**レコードセットの並べ替え**方法を使用して、親**レコードセット**を並べ替えることができます。  
  
 開いている親 **レコードセット** 内を移動し、子詳細 **レコードセット** オブジェクトにアクセスできるようになりました。 詳細については、「 [階層レコードセット内の行へのアクセス](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)」を参照してください。  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>結果の親および子の詳細レコードセット  
  
### <a name="parent"></a>Parent  
  
|SUM (rs.作成|rs|State|  
|---------------------------|--------|-----------|  
|130万|Child1 への参照|CA|  
|120万|Child2 への参照|WA|  
|110万|Child3 への参照|OR|  
  
## <a name="child1"></a>Child1  
  
|State|City|[母集団]|  
|-----------|----------|----------------|  
|CA|Los Angeles|80万|  
|CA|San Diego|60万|  
  
## <a name="child2"></a>Child2  
  
|State|City|[母集団]|  
|-----------|----------|----------------|  
|WA|Seattle|70万|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|State|City|[母集団]|  
|-----------|----------|----------------|  
|OR|Medford|200,000|  
|OR|Portland|400,000|  
|OR|Corvallis|300,000|  
  
## <a name="see-also"></a>参照  
 [階層レコードセット内の行へのアクセス](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [データシェイプの概要](../../../ado/guide/data/data-shaping-overview.md)   
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)   
 [仮形の文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [データシェイプに必要なプロバイダー](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 句](../../../ado/guide/data/shape-append-clause.md)   
 [一般的なシェイプコマンド](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value プロパティ (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications の関数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
