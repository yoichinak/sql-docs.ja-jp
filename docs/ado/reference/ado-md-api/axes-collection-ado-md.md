---
description: Axes コレクション (ADO MD)
title: Axes コレクション (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
author: rothja
ms.author: jroth
ms.openlocfilehash: 757d833da689c3d5097540571074292ec1bd2d69
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166189"
---
# <a name="axes-collection-ado-md"></a>Axes コレクション (ADO MD)
セルセットを定義する [軸](./axis-object-ado-md.md) オブジェクトを格納します。  
  
## <a name="remarks"></a>コメント  
 [Cellset](./cellset-object-ado-md.md)オブジェクトには、 **Axes** コレクションが含まれています。 **セルセット** を開くと、このコレクションには少なくとも1つの **軸** が含まれます。 **軸** オブジェクトの使用方法の詳細については、 [axis](./axis-object-ado-md.md)オブジェクトに関する説明を参照してください。  
  
> [!NOTE]
>  **セルセット** のフィルター軸が **Axes** コレクションに含まれていません。 詳細については、 [Filteraxis](./filteraxis-property-ado-md.md) プロパティを参照してください。  
  
 **軸** は、標準の ADO コレクションです。 コレクションのプロパティとメソッドを使用して、次の操作を実行できます。  
  
-   [Count](../ado-api/count-property-ado.md)プロパティを使用して、コレクション内のオブジェクトの数を取得します。  
  
-   既定の [Item](../ado-api/item-property-ado.md) プロパティを使用して、コレクションからオブジェクトを返します。  
  
-   [更新](../ado-api/refresh-method-ado.md)メソッドを使用して、プロバイダーからコレクション内のオブジェクトを更新します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [セルセットの例 (VB)](./cellset-example-vb.md)   
 [Axis オブジェクト (ADO MD)](./axis-object-ado-md.md)