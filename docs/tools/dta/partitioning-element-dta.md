---
title: Partitioning 要素 (DTA)
description: dta ユーティリティでは、Partitioning 要素に、データベース エンジン チューニング アドバイザーでの分析時に使用するパーティション分割構成が含まれます。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 7dc261ca057aeebe07cf8dbd8cb4a735f05ffbce
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100335961"
---
# <a name="partitioning-element-dta"></a>Partitioning 要素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

データベース エンジン チューニング アドバイザーでの分析時に使用するパーティション分割構成が含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特徴|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|**string**、長さは無制限です。|  
|**指定できる値**|**NONE**<br /> パーティション分割なし。<br /><br /> **FULL**<br /> 完全パーティション分割 (パフォーマンスが向上します)。<br /><br /> **ALIGNED**<br /> 固定パーティション分割 (管理が容易になります)。<br /><br /> この要素では、上記の値のいずれか 1 つを使用してください。<br /><br /> **ALIGNED** の場合、データベース エンジン チューニング アドバイザーによって生成される推奨設定では、すべての推奨インデックスが、インデックス定義の基になるテーブルとまったく同じ方法で分割されます。 インデックス付きビューの非クラスター化インデックスは、インデックス付きビューに準じます。|  
|**既定値**|**NONE**|  
|**個数**|**TuningOptions** 要素につき 1 回の出現が必要です。ただし、 **DropOnlyMode** 要素を使用している場合は別です。 **DropOnlyMode** を使用している場合は、 **Partitioning** を使用できません。 これらの要素を同時に指定することはできません。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[TuningOptions 要素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子要素**|[なし] :|  
  
## <a name="example"></a>例  
 この要素の使用例については、「[XML 入力ファイルの簡単なサンプル &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
