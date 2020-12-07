---
description: AddNew メソッドを使用したレコードの追加
title: AddNew | を使用したレコードの追加Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
author: rothja
ms.author: jroth
ms.openlocfilehash: 408f93b0054709de09d5556be94371dd9adc472f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991763"
---
# <a name="adding-records-using-addnew-method"></a>AddNew メソッドを使用したレコードの追加
**AddNew**メソッドの基本構文を次に示します。

 *レコードセット*。AddNew *FieldList*、 *Values*

 *FieldList*引数と*Values*引数は省略可能です。 *FieldList* は、単一の名前または名前の配列、または新しいレコード内のフィールドの序数位置のいずれかです。

 *Values*引数は、単一の値か、新しいレコードのフィールドの値の配列です。

 通常、1つのレコードを追加する場合は、引数を指定せずに **AddNew** メソッドを呼び出します。 具体的には、 **AddNew**を呼び出します。新しいレコードの各フィールドの **値** を設定します。次に、 **Update** または **UpdateBatch**、あるいはその両方を呼び出します。 **レコードセット**が、 **adaddnew**列挙定数と共に**サポート**プロパティを使用して、新しいレコードの追加をサポートしていることを確認できます。

 次のコードでは、この方法を使用して、サンプル **レコードセット**に新しい出荷業者を追加します。 SQL Server には、ShipperID フィールドの値が自動的に入力されます。 このため、このコードでは、新しいレコードのフィールド値を指定しようとしません。

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>解説
 このコードでは、バッチモードでクライアント側カーソルを使用して、切断された**レコードセット**を使用するため、 **UpdateBatch**メソッドを呼び出して変更をデータベースにポストする前に、新しい**接続**オブジェクトを使用して**レコードセット**をデータソースに再接続する必要があります。 これは、新しい関数 **Getnewconnection**を使用して簡単に行うことができます。
