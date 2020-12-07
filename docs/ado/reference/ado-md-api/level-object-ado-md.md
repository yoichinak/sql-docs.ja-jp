---
description: Level オブジェクト (ADO MD)
title: Level オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
author: rothja
ms.author: jroth
ms.openlocfilehash: 34dc7bc7eb6d80b3ec50cb1838cda0d0e419053b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986513"
---
# <a name="level-object-ado-md"></a>Level オブジェクト (ADO MD)
にはメンバーのセットが含まれており、各メンバーは階層内で同じランクを持ちます。  
  
## <a name="remarks"></a>解説  
 **Level**オブジェクトのコレクションとプロパティを使用して、次の操作を実行できます。  
  
-   [Name](./name-property-ado-md.md)プロパティと[UniqueName](./uniquename-property-ado-md.md)プロパティを使用して、**レベル**を識別します。  
  
-   [キャプション](./caption-property-ado-md.md)プロパティを使用して**レベル**を表示するときに使用する文字列を返します。  
  
-   [Description](./description-property-ado-md.md)プロパティを使用して、**レベル**を説明する意味のある文字列を返します。  
  
-   [メンバー](./members-collection-ado-md.md)コレクションを使用して、**レベル**を構成する[メンバー](./member-object-ado-md.md)オブジェクトを返します。  
  
-   [Depth](./depth-property-ado-md.md)プロパティを使用して、**レベル**のルートからレベル数を返します。  
  
-   標準の ADO [プロパティ](../ado-api/properties-collection-ado.md) コレクションを使用して、 **Level** オブジェクトに関する追加情報を取得します。  
  
 **Properties**コレクションには、プロバイダーが提供するプロパティが含まれています。 次の表に、使用可能なプロパティを示します。 実際のプロパティリストは、プロバイダーの実装によって異なる場合があります。 使用できるプロパティの詳細な一覧については、プロバイダーのドキュメントを参照してください。  
  
|Name|説明|  
|----------|-----------------|  
|CatalogName|このキューブが所属するカタログの名前。|  
|CubeName|キューブの名前。|  
|説明|レベルのわかりやすい説明。|  
|DimensionUniqueName|[ディメンション](./dimension-object-ado-md.md)の明確な名前です。|  
|HierarchyUniqueName|階層の明確な名前。|  
|LevelCaption|レベルに関連付けられているラベルまたはキャプション。|  
|LevelCardinality|レベル内のメンバーの数。|  
|LevelGUID|レベルの GUID。|  
|LevelName|レベルの名前。|  
|LevelNumber|階層のレベルとルートとの間の距離。|  
|LevelType|レベルの種類。|  
|LevelUniqueName|レベルの明確な名前。|  
|SchemaName|このキューブが所属するスキーマの名前です。|  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [CubeDef の例 (VBScript)](./cubedef-example-vbscript.md)   
 [Hierarchy オブジェクト (ADO MD)](./hierarchy-object-ado-md.md)   
 [Levels コレクション (ADO MD)](./levels-collection-ado-md.md)   
 [Members コレクション (ADO MD)](./members-collection-ado-md.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)