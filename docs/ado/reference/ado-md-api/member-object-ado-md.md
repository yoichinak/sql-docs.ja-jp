---
description: Member オブジェクト (ADO MD)
title: Member オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
author: rothja
ms.author: jroth
ms.openlocfilehash: 784dd3e842547c97f26107beaec67767363ce4ea
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986463"
---
# <a name="member-object-ado-md"></a>Member オブジェクト (ADO MD)
キューブ内のレベルのメンバー、レベルのメンバーの子、またはセルセットの軸に沿った位置のメンバーを表します。  
  
## <a name="remarks"></a>解説  
 メンバーのプロパティは、 **メンバー** が使用されているコンテキストによって異なります。 [CubeDef](./cubedef-object-ado-md.md)の[レベル](./level-object-ado-md.md)の**メンバー**には、現在の**メンバー**から階層内の次の下位レベルにある**メンバー**を返す[Children](./children-property-ado-md.md)プロパティがあります。 [位置](./position-object-ado-md.md)の**メンバー**の場合、**子**コレクションは常に空です。 また、 [Type](./type-property-ado-md.md)プロパティは、**レベル**の**メンバー**にのみ適用されます。  
  
 **Position**の**メンバー**には、[セルセット](./cellset-object-ado-md.md)を表示するときに便利な2つのプロパティがあります。 [Drilleddown](./drilleddown-property-ado-md.md)および[parentsameasprev](./parentsameasprev-property-ado-md.md)。 **レベル**の**メンバー**でこれらのプロパティにアクセスすると、エラーが発生します。  
  
 **レベル**の**メンバー**オブジェクトのコレクションとプロパティを使用して、次の操作を実行できます。  
  
-   [Name](./name-property-ado-md.md)プロパティと[UniqueName](./uniquename-property-ado-md.md)プロパティを使用して**メンバー**を識別します。  
  
-   [Caption](./caption-property-ado-md.md)プロパティを使用して**メンバー**を表示するときに使用する文字列を返します。  
  
-   [Description](./description-property-ado-md.md)プロパティを持つメジャーまたは数式**メンバー**を表す意味のある文字列を返します。  
  
-   [Type](./type-property-ado-md.md)プロパティを使用して**メンバー**の性質を判断します。  
  
-   [Leveldepth](./leveldepth-property-ado-md.md)プロパティと[leveldepth](./levelname-property-ado-md.md)プロパティを使用して、**メンバー**の**レベル**に関する情報を取得します。  
  
-   [親](./parent-property-ado-md.md)と[子](./children-property-ado-md.md)のプロパティを使用して、[階層](./hierarchy-object-ado-md.md)内の関連する**メンバー**を取得します。  
  
-   [Childcount](./childcount-property-ado-md.md)プロパティを使用して**メンバー**の子をカウントします。  
  
-   標準の ADO [プロパティ](../ado-api/properties-collection-ado.md) コレクションを使用して、 **Level** オブジェクトに関する追加情報を取得します。  
  
 [軸](./axis-object-ado-md.md)に沿った**位置**の**メンバー**のコレクションとプロパティを使用して、次の操作を実行できます。  
  
-   [Name](./name-property-ado-md.md)プロパティと[UniqueName](./uniquename-property-ado-md.md)プロパティを使用して**メンバー**を識別します。  
  
-   [Caption](./caption-property-ado-md.md)プロパティを使用して**メンバー**を表示するときに使用する文字列を返します。  
  
-   [Description](./description-property-ado-md.md)プロパティを持つメジャーまたは数式**メンバー**を表す意味のある文字列を返します。  
  
-   [Leveldepth](./leveldepth-property-ado-md.md)プロパティと[leveldepth](./levelname-property-ado-md.md)プロパティを使用して、**メンバー**の**レベル**に関する情報を取得します。  
  
-   [Childcount](./childcount-property-ado-md.md)プロパティを使用して**メンバー**の子をカウントします。  
  
-   この**メンバー**の直後にある**軸**に少なくとも1つの子があるかどうかを判断するには、 [drilの下](./drilleddown-property-ado-md.md)のプロパティを使用します。  
  
-   この**メンバー**の親が直前の**メンバー**の親と同じであるかどうかを判断するには、 [parentsameasprev](./parentsameasprev-property-ado-md.md)プロパティを使用します。  
  
-   標準の ADO [プロパティ](../ado-api/properties-collection-ado.md) コレクションを使用して、 **Level** オブジェクトに関する追加情報を取得します。  
  
 **Properties**コレクションには、プロバイダーが提供するプロパティが含まれています。 次の表に、使用可能なプロパティを示します。 実際のプロパティリストは、プロバイダーの実装によって異なる場合があります。 使用できるプロパティの詳細な一覧については、プロバイダーのドキュメントを参照してください。  
  
|Name|説明|  
|----------|-----------------|  
|CatalogName|このキューブが所属するカタログの名前。|  
|ChildrenCardinality|メンバーが持つ子の数。|  
|CubeName|キューブの名前。|  
|説明|メンバーのわかりやすい説明。|  
|DimensionUniqueName|[ディメンション](./dimension-object-ado-md.md)の明確な名前です。|  
|HierarchyUniqueName|階層の明確な名前。|  
|LevelNumber|階層のレベルとルートとの間の距離。|  
|LevelUniqueName|レベルの明確な名前。|  
|MemberCaption|メンバーに関連付けられたラベルまたはキャプション。|  
|MemberGUID|メンバーの GUID。|  
|メンバー名|メンバーの名前。|  
|MemberOrdinal|メンバーの序数。|  
|MemberType|メンバーの種類。|  
|MemberUniqueName|メンバーの明確な名前。|  
|ParentCount|このメンバーが持つ親の数。|  
|ParentLevel|メンバーの親のレベル番号。|  
|ParentUniqueName|メンバーの親の明確な名前。|  
|SchemaName|このキューブが所属するスキーマの名前です。|  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [カタログの例 (VB)](./catalog-example-vb.md)   
 [Members コレクション (ADO MD)](./members-collection-ado-md.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)