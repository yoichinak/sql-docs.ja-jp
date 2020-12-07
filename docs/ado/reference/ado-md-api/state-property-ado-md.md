---
description: State プロパティ (ADO MD)
title: State プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
author: rothja
ms.author: jroth
ms.openlocfilehash: 78b96e242cc27d27326d97f51cf378d9c5cbb51e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985983"
---
# <a name="state-property-ado-md"></a>State プロパティ (ADO MD)
セルセットの現在の状態を示します。  
  
## <a name="return-values"></a>戻り値  
 [セルセット](./cellset-object-ado-md.md)オブジェクトの現在の条件を示す**長**整数を返し、読み取り専用です。 有効な値は次のとおりです: **adStateClosed** (0) と **adstateopen** (1)。  
  
## <a name="remarks"></a>解説  
 [ObjectStateEnum](../ado-api/objectstateenum.md)定数名を使用するには、プロジェクトで ADO タイプライブラリが参照されている必要があります。 詳細については、「 [USING ADO with ADO MD](../../guide/multidimensional/using-ado-with-ado-md.md) 」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [CellSet オブジェクト (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [Close メソッド (ADO MD)](./close-method-ado-md.md)   
 [Open メソッド (ADO MD)](./open-method-ado-md.md)