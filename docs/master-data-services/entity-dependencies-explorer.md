---
description: エンティティの依存関係エクスプローラー
title: エンティティの依存関係エクスプローラー
ms.custom: ''
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- マスター データ サービス
ms.assetid: 9d922118-1412-4a9d-9c02-70d6c48d6c0d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e0b20fde852e02662780f75bd14e4b9023e01d80
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192410"
---
# <a name="entity-dependencies-explorer"></a>エンティティの依存関係エクスプローラー

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 2016 では、[エンティティの依存性] という新しいエクスプローラー ページが追加されました。ここでは、最初に派生階層を定義することなく、ドメイン ベースの属性 (DBA) 値で指定したとおりに、モデル内のエンティティ メンバー間のリレーションシップを視覚化する別の方法を提供します。   
  
これは、"自分のエンティティを誰が、どのように使用しているか" という質問に回答するために役立ちます。 このビューは、[派生階層] エクスプローラー ページと同様ですが、さらに包括的です。 ここでは、特定の階層の一部として定義された内容だけでなく、すべての DBA リレーションシップが表示されます。 表示されている階層構造は既存の DBS から単純に推定されるため、階層の定義は必要ありません。  
  
[エクスプローラー] ページで、[エンティティの依存関係] メニュー項目には、少なくとも 1 つのエンティティが依存する (つまり、少なくとも 1 つのエンティティに一覧されたエンティティを参照する DBA がある) モデルにあるすべてのエンティティが一覧表示されます。 依存関係 (直接と間接の両方) の数は、エンティティ名の横に表示されます。リストはこの数値によって並べ替えられ、最も頻繁に参照されるエンティティが上部に表示されます。 [サンプル データ](./sql-server-samples-model-deployment-packages-mds.md)のカスタマー モデルから取得された次のスクリーンショットでは、7 つのエンティティによって (直接または間接的に) 参照される BigArea エンティティを示します。  
  
![MDS_EntityDependencies_Menu.jpg](../master-data-services/media/mds-entitydependencies-menu-jpg.jpg)  
    
このメニュー項目をクリックすると、BigArea エンティティの新しい [エンティティの依存関係] エクスプローラーが開き、エンティティ メンバーがどのように使用されるかを表示します。 ツリーの上部に BigArea メンバーの階層ビューが表示され、次のように 7 つの入れ子になった使用中のエンティティのメンバーがあります。  
  
![MDS_EntityDependencies_Tree.jpg](../master-data-services/media/mds-entitydependencies-tree-jpg.jpg)  
    
エンティティは複数のエンティティから直接使用される場合があります。 上述の例では、SubRegion と RegionClimate の両方のエンティティが、Region エンティティ (に対する DBA 参照があり) を使用しています。 使用している各エンティティの数は、エンティティ名を持つ親ノードの下でグループ化されます。   
  
![MDS_EntityDependencies_Entity_Node.jpg](../master-data-services/media/mds-entitydependencies-entity-node-jpg.jpg)  
  
これらのコンテナー ツリー ノードには、エンティティ名の左側にグリッドのようなアイコンがあり、テキストは階層レベルの深さによって色分けされます。 上述の例では、SubRegion "CDSR {Canada}" には Region "CDR {Canada}" への DBA 参照があり、この Region は Area "CDA {Canada}" を参照し、この Area は BigArea "NAm {N. America}" を参照することを示します。  
  
このビューは、[階層] エクスプローラー ページのように、自由に編集することができます。 親子のリレーションシップは、子のメンバーを 1 つの親から別の親に切り取り/貼り付けたり、ドラッグ アンド ドロップしたりして、ツリーを変更することができます。 その他のメンバーの属性値は、ツリーの右側にある [詳細] パネルで変更できます。   
  
  
  
