---
title: KeepExisting 要素 (DTA)
description: dta ユーティリティでは、KeepExisting 要素により、データベース エンジン チューニング アドバイザーで推奨設定を生成するときに保持される物理設計構造を指定します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 829500f7335d1cb805b309ef642e6f70393b6912
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345903"
---
# <a name="keepexisting-element-dta"></a>KeepExisting 要素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

データベース エンジン チューニング アドバイザーが、推奨設定を生成するときに保持しなければならない物理設計構造 (インデックス、インデックス付きビュー、パーティション分割) を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特徴|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|**string**。長さの制限は、サーバーによって決まります。|  
|**指定できる値**|**NONE**<br /> 既存の構造を保持しません。<br /><br /> **ALL**<br /> 既存の構造をすべて保持します。<br /><br /> **ALIGNED**<br /> パーティションで固定された構造をすべて保持します。<br /><br /> **CL_IDX**<br /> テーブルのクラスター化インデックスをすべて保持します。<br /><br /> **IDX**<br /> テーブルのクラスター化インデックスと非クラスター化インデックスをすべて保持します。<br /><br /> この要素では、上記の値のいずれか 1 つを使用してください。|  
|**既定値**|[なし] :|  
|**個数**|省略可能。 **TuningOptions** 要素につき 1 回だけ使用できます。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[TuningOptions 要素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子要素**|[なし] :|  
  
## <a name="example"></a>例  
 この要素の使用例については、「[XML 入力ファイルの簡単なサンプル &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
