---
description: 非パラメーター化コマンドの操作
title: パラメーター化されていないコマンドの操作 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
author: rothja
ms.author: jroth
ms.openlocfilehash: c4e1187a319b086f7a28d3b282869271cd444ab5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980163"
---
# <a name="operation-of-non-parameterized-commands"></a>非パラメーター化コマンドの操作
パラメーター化されていないコマンドの場合は、すべてのプロバイダーコマンドが実行され、コマンドの実行時に **レコードセット** が作成されます。 コマンドを同期的に実行すると、すべての **レコードセット** が完全に設定されます。 非同期作成モードを選択した場合、 **レコードセット** の設定された状態は、作成モードと **レコードセット**のサイズによって異なります。  
  
 たとえば、 *親コマンド* を使用すると、customers テーブルから会社の顧客の **レコードセット** を返すことができます。また、 *child コマンド* は、orders テーブルのすべての顧客に対して、注文の **レコードセット** を返すことができます。  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 パラメーター化されていない親子リレーションシップの場合、各親および子の **Recordset** オブジェクトは、それらを関連付けるために共通の列を持つ必要があります。 列の名前は、関連句、 *親列* 、および *子列*になります。 列の名前はそれぞれの **レコードセット** オブジェクトによって異なる場合がありますが、意味のある関係を指定するためには、同じ情報を参照する必要があります。 たとえば、 **Customers** および **Orders レコードセット** オブジェクトは、どちらも customerID フィールドを持つことができます。 子 **レコードセット** のメンバーシップはプロバイダーコマンドによって決定されるので、子 **レコードセット** に孤立した行を含めることができます。 これらの孤立した行には、追加のリシェイプなしでアクセスできません。  
  
 データシェイプによって、チャプター列が親 **レコードセット**に追加されます。 チャプター列の値は、関連付け句を満たす子 **レコードセット**内の行を参照します。 つまり、同じ値が、指定された親行の *親列* にあります。これは、チャプターの子のすべての行の *子列* にあります。 同じ関連句で複数の TO 句を使用すると、AND 演算子を使用して暗黙的に結合されます。 関連付け句の親列が親 **レコードセット**のキーを構成していない場合、1つの子行に複数の親行を含めることができます。  
  
 チャプター列の参照にアクセスすると、その参照によって表される **レコードセット** が ADO によって自動的に取得されます。 パラメーター化されていないコマンドでは、子 **レコードセット** 全体が取得されていますが、この章では行のサブセットのみを提示していることに注意してください。  
  
 付加列に *chapter エイリアス*がない場合は、自動的に名前が生成されます。 列の [フィールド](../../reference/ado-api/field-object.md) オブジェクトが **レコードセット** オブジェクトの [Fields](../../reference/ado-api/fields-collection-ado.md) コレクションに追加され、そのデータ型は **adchapter**になります。  
  
 階層 **レコードセット**の移動の詳細については、「 [階層レコードセット内の行へのアクセス](./accessing-rows-in-a-hierarchical-recordset.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データシェイプの例](./data-shaping-example.md)   
 [仮形の文法](./formal-shape-grammar.md)   
 [一般的な Shape コマンド](./shape-commands-in-general.md)