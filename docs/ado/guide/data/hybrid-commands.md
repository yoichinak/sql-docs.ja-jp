---
description: ハイブリッド コマンド
title: ハイブリッドコマンド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- hybrid commands [ADO]
- data shaping [ADO], hybrid commands
ms.assetid: e8ca40e8-459c-40e2-8dd3-3ec6d5ee7b51
author: rothja
ms.author: jroth
ms.openlocfilehash: ec23a74b26be84684965c8e81fffbfd827a9981a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980513"
---
# <a name="hybrid-commands"></a>ハイブリッド コマンド
ハイブリッドコマンドは、部分的にパラメーター化されたコマンドです。 次に例を示します。  
  
```  
SHAPE {select * from plants}   
   APPEND( {select * from customers where country = ?}   
           RELATE PlantCountry TO PARAMETER 0,   
             PlantRegion TO CustomerRegion )   
```  
  
 ハイブリッドコマンドのキャッシュ動作は、通常のパラメーター化コマンドと同じです。  
  
## <a name="see-also"></a>参照  
 [データシェイプの例](./data-shaping-example.md)   
 [仮形の文法](./formal-shape-grammar.md)   
 [一般的な Shape コマンド](./shape-commands-in-general.md)