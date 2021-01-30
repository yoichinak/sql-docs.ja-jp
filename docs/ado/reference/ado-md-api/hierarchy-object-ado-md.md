---
description: Hierarchy オブジェクト (ADO MD)
title: Hierarchy オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
author: rothja
ms.author: jroth
ms.openlocfilehash: a1370f83c4214047038eadf4b84813f0b48c3b72
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99164544"
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy オブジェクト (ADO MD)
[ディメンション](./dimension-object-ado-md.md)のメンバーを集計または "ロールアップ" できる1つの方法を表します。 ディメンションは、1つまたは複数の階層に沿って集計できます。  
  
## <a name="remarks"></a>コメント  
 **Hierarchy** オブジェクトのコレクションとプロパティを使用して、次の操作を実行できます。  
  
-   [Name](./name-property-ado-md.md)プロパティと [UniqueName](./uniquename-property-ado-md.md)プロパティを使用して、**階層** を識別します。  
  
-   [Description](./description-property-ado-md.md)プロパティを使用して **階層** を説明する意味のある文字列を返します。  
  
-   [レベルコレクションを](./levels-collection-ado-md.md)持つ **階層** を構成する [Level](./level-object-ado-md.md)オブジェクトを返します。  
  
-   標準の ADO [プロパティ](../ado-api/properties-collection-ado.md) コレクションを使用して、 **Hierarchy** オブジェクトに関する追加情報を取得します。  
  
 **Properties** コレクションには、プロバイダーが提供するプロパティが含まれています。 次の表に、使用可能なプロパティを示します。 実際のプロパティリストは、プロバイダーの実装によって異なる場合があります。 使用できるプロパティの詳細な一覧については、プロバイダーのドキュメントを参照してください。  
  
|名前|説明|  
|----------|-----------------|  
|AllMember|階層内のロールアップの最上位レベルにあるメンバー。|  
|CatalogName|このキューブが所属するカタログの名前。|  
|CubeName|キューブの名前。|  
|DefaultMember|この階層の既定のメンバーの一意の名前。|  
|説明|階層についてのわかりやすい説明。|  
|DimensionType|この階層が属するディメンションの種類。|  
|DimensionUniqueName|ディメンションの明確な名前です。|  
|HierarchyCaption|階層に関連付けられたラベルまたはキャプション。|  
|HierarchyCardinality|階層内のメンバーの数。|  
|HierarchyGUID|階層の GUID。|  
|HierarchyName|階層の名前。|  
|HierarchyUniqueName|階層の明確な名前。|  
|SchemaName|このキューブが所属するスキーマの名前です。|  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [CubeDef の例 (VBScript)](./cubedef-example-vbscript.md)   
 [Dimension オブジェクト (ADO MD)](./dimension-object-ado-md.md)   
 [Hierarchy コレクション (ADO MD)](./hierarchies-collection-ado-md.md)   
 [Levels コレクション (ADO MD)](./levels-collection-ado-md.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)