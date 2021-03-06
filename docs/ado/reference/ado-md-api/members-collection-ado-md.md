---
description: Members コレクション (ADO MD)
title: Members コレクション (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: rothja
ms.author: jroth
ms.openlocfilehash: d628481607e05c2278e5dd1beede08a12b93d740
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054497"
---
# <a name="members-collection-ado-md"></a>Members コレクション (ADO MD)
レベルまたは軸に沿った位置からの [メンバー](./member-object-ado-md.md) オブジェクトを格納します。  
  
## <a name="remarks"></a>解説  
 **メンバー** コレクションは、次の種類のメンバーを格納するために使用されます。  
  
-   キューブ内のレベルを構成するメンバー。 これらは、 [Level](./level-object-ado-md.md)オブジェクトの **Members** コレクションに含まれています。 たとえば、 [多次元スキーマとデータの概要](../../guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)からサンプルを使用すると、国レベルの4つのメンバーがカナダ、USA、英国、およびドイツになります。  
  
-   階層内の特定のメンバーの子であるメンバー。 これらのメンバーは、親 **メンバー** オブジェクトの [Children](./children-property-ado-md.md)プロパティによって返されます。 たとえば、同じサンプルを使用すると、カナダのメンバーの2つの子が Canada-East とカナダ西部になります。  
  
-   [セルセット](./cellset-object-ado-md.md)の軸に沿って特定の位置を定義するメンバー。 例として、セルセットを使用して [多次元データを操作](../../guide/multidimensional/working-with-multidimensional-data.md) する場合、x 軸の最初の位置の2つのメンバーはバレンタインと Seattle です。 これらのメンバーは、 [Position](./position-object-ado-md.md)オブジェクトの **members** コレクションに含まれています。  
  
 **メンバー** は、標準の ADO コレクションです。 コレクションのプロパティとメソッドを使用して、次の操作を実行できます。  
  
-   [Count](../ado-api/count-property-ado.md)プロパティを使用して、コレクション内のオブジェクトの数を取得します。  
  
-   既定の [Item](../ado-api/item-property-ado.md) プロパティを使用して、コレクションからオブジェクトを返します。  
  
-   [更新](../ado-api/refresh-method-ado.md)メソッドを使用して、プロバイダーからコレクション内のオブジェクトを更新します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Members の例 (VBScript)](./members-example-vbscript.md)   
 [Member オブジェクト (ADO MD)](./member-object-ado-md.md)