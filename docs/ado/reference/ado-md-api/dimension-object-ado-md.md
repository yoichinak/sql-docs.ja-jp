---
description: Dimension オブジェクト (ADO MD)
title: Dimension オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
author: rothja
ms.author: jroth
ms.openlocfilehash: f034dd2bea6b7b37f69dcff58013263ec9ba5187
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986883"
---
# <a name="dimension-object-ado-md"></a>Dimension オブジェクト (ADO MD)
メンバーの1つ以上の階層を含む多次元キューブのディメンションの1つを表します。  
  
## <a name="remarks"></a>解説  
 **ディメンション**オブジェクトのコレクションとプロパティを使用して、次の操作を実行できます。  
  
-   [Name](./name-property-ado-md.md)プロパティと[UniqueName](./uniquename-property-ado-md.md)プロパティを使用して、**ディメンション**を識別します。  
  
-   [Description](./description-property-ado-md.md)プロパティを使用して、**ディメンション**を説明する意味のある文字列を返します。  
  
-   Hierarchy[コレクションを使用して](./hierarchies-collection-ado-md.md)、**ディメンション**を構成する[階層](./hierarchy-object-ado-md.md)オブジェクトを返します。  
  
-   標準の ADO [プロパティ](../ado-api/properties-collection-ado.md) コレクションを使用して、 **ディメンション** オブジェクトに関する追加情報を取得します。  
  
 **Properties**コレクションには、プロバイダーが提供するプロパティが含まれています。 次の表に、使用可能なプロパティを示します。 実際のプロパティリストは、プロバイダーの実装によって異なる場合があります。 使用できるプロパティの詳細な一覧については、プロバイダーのドキュメントを参照してください。  
  
|Name|説明|  
|----------|-----------------|  
|CatalogName|このキューブが所属するカタログの名前。|  
|CubeName|キューブの名前。|  
|DefaultHierarchy|既定の階層の一意の名前。|  
|説明|キューブについてのわかりやすい説明。|  
|DimensionCaption|ディメンションに関連付けられているラベルまたはキャプション。|  
|DimensionCardinality|ディメンション内のメンバーの数。|  
|DimensionGUID|ディメンションの GUID。|  
|DimensionName|次元の名前。|  
|DimensionOrdinal|キューブを形成するディメンションのグループ間のディメンションの序数です。|  
|DimensionType|ディメンションの種類。|  
|DimensionUniqueName|ディメンションの明確な名前です。|  
|SchemaName|このキューブが所属するスキーマの名前です。|  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [CubeDef の例 (VBScript)](./cubedef-example-vbscript.md)   
 [CubeDef オブジェクト (ADO MD)](./cubedef-object-ado-md.md)   
 [Dimensions コレクション (ADO MD)](./dimensions-collection-ado-md.md)   
 [Hierarchy コレクション (ADO MD)](./hierarchies-collection-ado-md.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)