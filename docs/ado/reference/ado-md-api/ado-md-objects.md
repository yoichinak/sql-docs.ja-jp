---
description: ADO MD オブジェクト
title: ADO MD オブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
author: rothja
ms.author: jroth
ms.openlocfilehash: a75672db242d5b7388eb625bc028728c8522b11c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987433"
---
# <a name="ado-md-objects"></a>ADO MD オブジェクト

|Object|説明|  
|-|-|  
|[軸](./axis-object-ado-md.md)|1つ以上のディメンションの選択されたメンバーを含むセルセットの位置指定軸またはフィルター軸を表します。|  
|[カタログ](./catalog-object-ado-md.md)|多次元データプロバイダー (.MDP) に固有の多次元スキーマ情報 (つまり、キューブおよび基になるディメンション、階層、レベル、およびメンバー) が含まれています。|  
|[Cell (セル)](./cell-object-ado-md.md)|セルセットに含まれる軸の座標の交差部分にあるデータを表します。|  
|[セルセット](./cellset-object-ado-md.md)|多次元クエリの結果を表します。 これは、キューブまたは他のセルセットから選択されたセルのコレクションです。|  
|[CubeDef](./cubedef-object-ado-md.md)|多次元スキーマから、関連するディメンションのセットを含むキューブを表します。|  
|[ディメンション](./dimension-object-ado-md.md)|メンバーの1つ以上の階層を含む多次元キューブのディメンションの1つを表します。|  
|[Hierarchy](./hierarchy-object-ado-md.md)|ディメンションのメンバーを集計または "ロールアップ" できる1つの方法を表します。 ディメンションは、1つまたは複数の階層に沿って集計できます。|  
|[Level](./level-object-ado-md.md)|にはメンバーのセットが含まれており、各メンバーは階層内で同じランクを持ちます。|  
|[メンバー](./member-object-ado-md.md)|キューブ内のレベルのメンバー、レベルのメンバーの子、またはセルセットの軸に沿った位置のメンバーを表します。|  
|[Position](./position-object-ado-md.md)|軸に沿って点を定義する、異なる次元の1つ以上のメンバーのセットを表します。|  
  
 また、 **カタログ** オブジェクトは、標準の ado ライブラリに含まれる ado **Connection** オブジェクトに接続されています。  
  
|Object|説明|  
|------------|-----------------|  
|[接続](../ado-api/connection-object-ado.md)|データ ソースへの開いた接続を表します。|  
  
 これらのオブジェクト間のリレーションシップは、 [ADO MD オブジェクトモデル](./ado-md-object-model.md)で示されています。  
  
 多くの ADO MD オブジェクトを対応するコレクションに含めることができます。 たとえば、 [CubeDef](./cubedef-object-ado-md.md)オブジェクトは、**カタログ**の[cubedefs](./cubedefs-collection-ado-md.md)コレクションに含めることができます。 詳細については、「 [ADO MD コレクション](./ado-md-collections.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ADO MD API リファレンス](./ado-md-object-model.md?view=sql-server-ver15)   
 [ADO MD コード例](./ado-md-code-examples.md)   
 [ADO MD コレクション](./ado-md-collections.md)   
 [ADO MD 列挙定数](./ado-md-enumerated-constants.md)   
 [ADO MD メソッド](./ado-md-methods.md)   
 [ADO MD オブジェクトモデル](./ado-md-object-model.md)   
 [ADO MD のプロパティ](./ado-md-properties.md)