---
description: ActiveCommand プロパティ (ADO)
title: ActiveCommand プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
author: rothja
ms.author: jroth
ms.openlocfilehash: df737543e8cc09735c7da413b89406b6f2385079
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977156"
---
# <a name="activecommand-property-ado"></a>ActiveCommand プロパティ (ADO)
関連付けられた[レコードセット](./recordset-object-ado.md)オブジェクトを作成した[Command](./command-object-ado.md)オブジェクトを示します。  
  
## <a name="return-value"></a>戻り値  
 **Command**オブジェクトを含む**Variant**を返します。 既定値は null オブジェクト参照です。  
  
## <a name="remarks"></a>解説  
 **Activecommand**プロパティは読み取り専用です。  
  
 **Command**オブジェクトを使用して現在の**レコードセット**を作成しなかった場合は、 **Null**オブジェクト参照が返されます。  
  
 このプロパティを使用して、結果の**レコードセット**オブジェクトだけを指定した場合に、関連付けられている**Command**オブジェクトを検索します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [ActiveCommand プロパティの例 (VB)](./activecommand-property-example-vb.md)   
 [ActiveCommand プロパティの例 (JScript)](./activecommand-property-example-jscript.md)   
 [ActiveCommand プロパティの例 (VC + +)](./activecommand-property-example-vc.md)   
 [Command オブジェクト (ADO)](./command-object-ado.md)