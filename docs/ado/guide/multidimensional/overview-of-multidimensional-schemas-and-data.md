---
description: 多次元スキーマとデータの概要
title: 多次元スキーマとデータの概要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: rothja
ms.author: jroth
ms.openlocfilehash: 431ff25d49c4a45055d796aba98f229564872a4e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978643"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>多次元スキーマとデータの概要
## <a name="understanding-multidimensional-schemas"></a>多次元スキーマについて  
 ADO MD の中央のメタデータオブジェクトは、 *キューブ*です。これは、関連するディメンション、階層、レベル、およびメンバーの構造化されたセットで構成されます。  
  
 *ディメンション*は、ビジネスエンティティから派生した多次元データベースのデータの独立したカテゴリです。 ディメンションには、通常、データベースのメジャーのクエリ条件として使用するアイテムが含まれています。  
  
 *階層*は、ディメンションの集計のパスです。 ディメンションには、親子リレーションシップを持つ複数レベルの粒度があります。 階層は、これらのレベルがどのように関連しているかを定義します。  
  
 *レベル*は、階層内の集計の手順です。 複数層の情報が含まれているディメンションの場合は、各レイヤーがレベルです。  
  
 *メンバー*とは、ディメンション内のデータアイテムのことです。 通常は、キャプションを作成するか、メンバーを使用してデータベースのメジャーを記述します。  
  
 キューブは ADO MD の [CubeDef](../../reference/ado-md-api/cubedef-object-ado-md.md) オブジェクトによって表されます。 ディメンション、階層、レベル、およびメンバーも、対応する ADO MD オブジェクト ( [ディメンション](../../reference/ado-md-api/dimension-object-ado-md.md)、 [階層](../../reference/ado-md-api/hierarchy-object-ado-md.md)、 [レベル](../../reference/ado-md-api/level-object-ado-md.md)、および [メンバー](../../reference/ado-md-api/member-object-ado-md.md)) によって表されます。  
  
### <a name="dimensions"></a>Dimensions  
 キューブのディメンションは、ビジネスエンティティと、データベースでモデル化されるデータの種類によって異なります。 通常、各ディメンションは、データを選択するための独立したエントリポイントまたはメカニズムです。  
  
 たとえば、売上データを含むキューブには、営業担当者、地理、時間、製品、メジャーの5つのディメンションがあります。 Measure ディメンションには実際の売上データ値が含まれ、他のディメンションは売上データ値を分類およびグループ化する方法を表します。  
  
 Geography ディメンションには、次のメンバーのセットがあります。  
  
```console
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>階層  
 階層は、ディメンションのレベルを "ロールアップ" またはグループ化する方法を定義します。 ディメンションには、複数の階層を含めることができます。 Geography ディメンションには自然階層が存在します。  
  
### <a name="levels"></a>レベル  
 前の図に示されている Geography ディメンションの例では、各ボックスは階層内のレベルを表します。  
  
 各レベルには、次のようにメンバーのセットがあります。  
  
-   世界 `= {All}`  
  
-   世界 `= {North America, Europe}`  
  
-   国々 `= {Canada, USA, UK, Germany}`  
  
-   報酬 `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   地域 `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>メンバー  
 階層のリーフレベルのメンバーには子がなく、ルートレベルのメンバーには親がありません。 他のすべてのメンバーには少なくとも1つの親と少なくとも1つの子があります。 たとえば、Geography ディメンションの階層ツリーを部分的に検査すると、次の親子関係が生成されます。  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 メンバーは、ディメンションごとに1つ以上の階層に沿って統合できます。 日レベルから年レベルにロールアップする2つの方法がある時間ディメンションを考えてみましょう。  
  
 この例では、もう1つの特性も示しています。週単位階層の週レベルの一部のメンバーは、Quarter 階層のどのレベルにも表示されません。 したがって、階層にはディメンションのすべてのメンバーを含める必要はありません。  
  
## <a name="see-also"></a>参照  
 [ADO MD オブジェクトモデル](../../reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多次元) (ADO MD)](./ado-multidimensional-ado-md.md)   
 [ADO MD を使用したプログラミング](./programming-with-ado-md.md)   
 [ADO MD での ADO の使用](./using-ado-with-ado-md.md)   
 [多次元データの操作](./working-with-multidimensional-data.md)