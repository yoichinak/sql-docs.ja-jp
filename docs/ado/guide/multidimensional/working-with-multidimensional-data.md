---
description: 多次元データの操作
title: 多次元データの操作 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: rothja
ms.author: jroth
ms.openlocfilehash: 0589b1fe5ca6da29f088e26b2236cfc5205bfe0c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978573"
---
# <a name="working-with-multidimensional-data"></a>多次元データの操作
*セルセット*は、多次元データに対するクエリの結果です。 これは、軸のコレクションで構成されており、通常は4つの軸を超えていません。通常は2つまたは3つです。 *軸*は、1つまたは複数のディメンションのメンバーのコレクションであり、キューブ内の特定の値を検索またはフィルター処理するために使用されます。  
  
 *位置*は、軸に沿ったポイントです。 1つのディメンションで構成される軸の場合、これらの位置はディメンションメンバーのサブセットになります。 1つの軸が複数の次元で構成されている場合、各位置は複合エンティティになります。ここで *、n は* 、その軸に沿った次元の数 *を示します* 。 位置の各部分は、1つの構成ディメンションのメンバーです。  
  
 たとえば、売上データを含むキューブの Geography および Product ディメンションが、セルセットの x 軸に沿って配置されている場合、この軸に沿った位置に、メンバー "USA" と "Computers" が含まれている可能性があります。 この例では、x 軸に沿って位置を決定するには、各次元のメンバーが軸に沿って配置されている必要があります。  
  
 *セル*は、軸の座標の交差部分に配置されるオブジェクトです。 各セルには、データ自体、書式設定された文字列 (表示可能な形式のセルデータ)、およびセルの序数値を含む、複数の情報が関連付けられています。 (各セルは、セルセット内の一意の序数値です。 セルセット内の最初のセルの序数値は0ですが、8つの列を持つセルセットの2番目の行の一番左のセルの序数値は8になります)。  
  
 たとえば、キューブには次の6つのディメンションがあります (このキューブスキーマは、 [「多次元スキーマとデータの概要](./overview-of-multidimensional-schemas-and-data.md)」で説明した例と若干異なることに注意してください)。  
  
-   Salesperson  
  
-   Geography (自然階層)-大陸、国、州など  
  
-   四半期、月、日  
  
-   Years  
  
-   メジャー-Sales、PercentChange、BudgetedSales  
  
-   製品  
  
 次のセルセットは、すべての製品の1991の売上を表します。  
  
> [!NOTE]
>  この例のセル値は、軸位置序数の順序付きペアとして表示できます。最初の桁は x 軸の位置を表し、2番目の数字は y 軸の位置を表します。  
  
 このセルセットの特性は次のとおりです。  
  
-   軸の寸法: 四半期、販売員、Geography  
  
-   ディメンションのフィルター選択: メジャー、年、製品  
  
-   2つの軸: 縦棒 (x, または軸 0) と行 (y または軸 1)  
  
-   x 軸: 2 つの入れ子になったディメンション、販売員、地理  
  
-   y 軸: 四半期ディメンション  
  
 X 軸には、販売員と地理の2つの入れ子になったディメンションがあります。 Geography から、4つのメンバーが選択されています。シアトル、ボストン、米国南部、および日本です。 販売員: バレンタインと Nash から2つのメンバーが選択されています。 これにより、この軸上に合計8個の位置 (8 = 4 * 2) が生成されます。  
  
 各座標は、2つのメンバーを持つ位置として表されます。1つは販売員ディメンションから、もう1つは Geography ディメンションです。  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 軸には、次の8つの位置を含むディメンションが1つだけあります。  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 セルセット、セル、軸、および位置はすべて、対応するオブジェクト (セルセット[、](../../reference/ado-md-api/cellset-object-ado-md.md)[セル](../../reference/ado-md-api/cell-object-ado-md.md)、[軸](../../reference/ado-md-api/axis-object-ado-md.md)、および[位置](../../reference/ado-md-api/position-object-ado-md.md)) によって ADO MD で表されます。  
  
## <a name="see-also"></a>参照  
 [ADO MD オブジェクトモデル](../../reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多次元) (ADO MD)](./ado-multidimensional-ado-md.md)   
 [多次元スキーマとデータの概要](./overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD を使用したプログラミング](./programming-with-ado-md.md)   
 [ADO MD と ADO の併用](./using-ado-with-ado-md.md)