---
description: リシェイプ
title: リシェイプ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
author: rothja
ms.author: jroth
ms.openlocfilehash: 04c43b9fcca56959aec242f344da6ec81a825030
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979773"
---
# <a name="reshaping"></a>リシェイプ
Shape コマンドの句によって作成された **レコードセット** には、(通常は as キーワードを使用して) *エイリアス* 名を割り当てることができます。 整形された **レコードセット** のエイリアスは、まったく別のコマンドで参照できます。 つまり、新しい shape コマンドで以前に整形された**レコードセット**を再利用*したり、* 再利用したりすることができます。 この機能をサポートするために、ADO ではプロパティの [リシェイプ名](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)が提供されています。  
  
 リシェイプには、主に2つの関数があります。 1つ目は、既存の **レコードセット** を新しい親 **レコードセット**に関連付けることです。  
  
## <a name="example"></a>例  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 2番目の関数は、構文 "SHAPE" を使用して、既存の子 **レコードセット** オブジェクトに対して非チャプターアクセスを有効にし \<recordset reshape name> ます。  
  
> [!NOTE]
>  既存の**レコードセット**に列を追加したり、いずれかの介在する COMPUTE 句でパラメーター化された**レコードセット**または**レコードセット**オブジェクトの形状をリシェイプしたり、または**レコードセット**からリシェイプさ**れるレコードセットの子孫に**対して集計操作を実行したりすることはできません。 リシェイプされる **レコードセット** と新しい shape コマンドは、両方とも同じ [接続](../../../ado/reference/ado-api/connection-object-ado.md)を使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [データ シェイプの例](../../../ado/guide/data/data-shaping-example.md)
