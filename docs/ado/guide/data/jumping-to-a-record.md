---
description: レコードへのジャンプ
title: レコードへのジャンプ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: rothja
ms.author: jroth
ms.openlocfilehash: 96987a5c51d7a888672609aa28f3fd223ccfffa1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980403"
---
# <a name="jumping-to-a-record"></a>レコードへのジャンプ
[Move](../../reference/ado-api/move-method-ado.md)メソッドを使用すると、次の構文を使用して、**レコードセット**内で指定した数のレコードを前方または後方に移動できます。  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>解説  
 **Move**メソッドは、すべての**レコードセット**オブジェクトでサポートされています。  
  
 *NumRecords*引数が0より大きい場合、現在のレコードの位置は (**レコードセット**の末尾に向かって) 前方に移動します。 *NumRecords*が0未満の場合、現在のレコードの位置は後方 (**レコードセット**の先頭に向かって) に移動します。  
  
 **移動**呼び出しによって、現在のレコード位置が最初のレコードの前のポイントに移動された場合、ADO では、レコード**セット**内の最初のレコード (**BOF**が**True**) の前の位置に現在のレコードが設定されます。 **BOF**プロパティが既に**True**の場合に後方に移動しようとすると、エラーが生成されます。  
  
 **移動**呼び出しによって、現在のレコード位置が最後のレコードの後のポイントに移動された場合、ADO は現在のレコードを**レコードセット**の最後のレコード (**EOF**が**True**) の後の位置に設定します。 **EOF**プロパティが既に**True**になっているときに先に進むと、エラーが発生します。  
  
 空の**レコードセット**オブジェクトから**Move**メソッドを呼び出すと、エラーが生成されます。  
  
 Start 引数にブックマークを渡すと、**レコードセット**オブジェクトがブックマークをサポートしていると仮定した場合、このブックマークを持つレコードに対する相対移動が*実行*されます。 ブックマークは、 [bookmark](../../reference/ado-api/bookmark-property-ado.md) プロパティを使用して取得します。 指定しない場合、移動は現在のレコードを基準にして行われます。  
  
 プロバイダーからローカルにレコードをキャッシュするために **CacheSize** プロパティを使用している場合は、現在のレコードの位置をキャッシュされたレコードの現在のグループの外側に移動する *NumRecords* 引数を渡すと、変換先レコードから始まる新しいレコードのグループが ADO によって強制的に取得されます。 **CacheSize**プロパティは、新しく取得したグループのサイズを決定し、宛先レコードは最初に取得されたレコードになります。