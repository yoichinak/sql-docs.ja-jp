---
description: CubeDef オブジェクト (ADO MD)
title: CubeDef オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
author: rothja
ms.author: jroth
ms.openlocfilehash: b9f25f238fd8c0637f86ff7fdf5d9fc17320fdf7
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054817"
---
# <a name="cubedef-object-ado-md"></a>CubeDef オブジェクト (ADO MD)
多次元スキーマから、関連するディメンションのセットを含むキューブを表します。  
  
## <a name="remarks"></a>解説  
 **CubeDef** オブジェクトのコレクションとプロパティを使用して、次の操作を行うことができます。  
  
-   [Name](./name-property-ado-md.md)プロパティを使用して **CubeDef** を識別します。  
  
-   [Description](./description-property-ado-md.md)プロパティを持つキューブを説明する文字列を返します。  
  
-   [ディメンション](./dimensions-collection-ado-md.md)コレクションを持つキューブを構成するディメンションを返します。  
  
-   標準の ADO [プロパティ](../ado-api/properties-collection-ado.md)コレクションを使用して、 **CubeDef** に関する追加情報を取得します。  
  
 **Properties** コレクションには、プロバイダーが提供するプロパティが含まれています。 次の表に、使用可能なプロパティを示します。 実際のプロパティリストは、プロバイダーの実装によって異なる場合があります。 使用できるプロパティの詳細な一覧については、プロバイダーのドキュメントを参照してください。  
  
|名前|説明|  
|----------|-----------------|  
|CatalogName|このキューブが所属するカタログの名前。|  
|CreatedOn|キューブ作成の日付と時刻。|  
|CubeGUID|キューブ GUID。|  
|CubeName|キューブの名前。|  
|CubeType|キューブの種類。|  
|DataUpdatedBy|前回のデータ更新を行っているユーザーのユーザー ID。|  
|説明|キューブについてのわかりやすい説明。|  
|LastSchemaUpdate|スキーマの最終更新日時。|  
|SchemaName|このキューブが所属するスキーマの名前です。|  
|SchemaUpdatedBy|前回のスキーマ更新を行っているユーザーのユーザー ID。|  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [CubeDef の例 (VBScript)](./cubedef-example-vbscript.md)   
 [Catalog オブジェクト (ADO MD)](./catalog-object-ado-md.md)   
 [CubeDefs コレクション (ADO MD)](./cubedefs-collection-ado-md.md)   
 [Dimensions コレクション (ADO MD)](./dimensions-collection-ado-md.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)