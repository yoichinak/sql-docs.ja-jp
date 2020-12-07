---
description: 介在する Shape COMPUTE 句
title: 中間図形の COMPUTE 句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- COMPUTE clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: a576bf81-8f3c-4ba1-817b-87e89a8da684
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a4be3fb7f70ba41e24cd757da34e7272e51f87c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980443"
---
# <a name="intervening-shape-compute-clauses"></a>介在する Shape COMPUTE 句
次の例に示すように、パラメーター化された shape コマンドで親と子の間に1つ以上の COMPUTE 句を埋め込むことが有効です。  
  
```  
SHAPE {select au_lname, state from authors} APPEND   
   ((SHAPE   
      (SHAPE   
         {select * from authors where state = ?} rs   
      COMPUTE rs, ANY(rs.state) state, ANY(rs.au_lname) au_lname   
      BY au_id) rs2   
   COMPUTE rs2, ANY(rs2.state) BY au_lname)   
RELATE state TO PARAMETER 0)  
```  
  
## <a name="see-also"></a>参照  
 [データシェイプの例](./data-shaping-example.md)   
 [仮形の文法](./formal-shape-grammar.md)   
 [一般的な Shape コマンド](./shape-commands-in-general.md)