---
title: DropOnlyMode 要素 (DTA)
description: dta ユーティリティでは、DropOnlyMode 要素により、データベース エンジン チューニング アドバイザーで既存のインデックス、インデックス付きビュー、またはパーティションの削除だけを対象にすることを指定します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 27d38719f0ee9572a86a7b196655489b33824071
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100351099"
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode 要素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

データベース エンジン チューニング アドバイザーのチューニング セッションで、既存のインデックス、インデックス付きビュー、パーティションの削除だけを対象にすることを指定します。 このチューニング オプションを指定すると、新しい物理設計構造は考慮の対象になりません。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
 **データ型と長さ**  
  
 **既定値**  
  
 **発生頻度**: 省略可能。 **TuningOptions** 要素につき 1 回のみ使用できます。 **TuningOptions** 要素内で以下の要素を指定する場合には使用できません。  
  
-   [FeatureSet 要素 &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning 要素 &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [KeepExisting 要素 &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md) が **ALL** に設定されている  
  
## <a name="element-relationships"></a>要素の関係  
 **親要素**:[TuningOptions 要素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
 **子要素**  
  
## <a name="example"></a>例  
 次の例は、データベース エンジン チューニング アドバイザーの XML 入力ファイルの、 **DropOnlyMode** が指定された **TuningOptions** セクションを示しています。 この例では、チューニング時間は 24 時間 (1440 分) に制限されており、既存のクラスター化インデックスおよび非クラスター化インデックスはすべて削除することが検討されます。  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
