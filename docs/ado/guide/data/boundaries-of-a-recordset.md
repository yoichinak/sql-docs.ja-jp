---
description: レコードセットの境界
title: Recordset | の境界Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
author: rothja
ms.author: jroth
ms.openlocfilehash: 2c0df560a7a70dd46c4a846e3271b5b5ea10584e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991593"
---
# <a name="boundaries-of-a-recordset"></a>レコードセットの境界
**レコードセット** では、データセットの先頭と末尾を区切るために、 **BOF** プロパティと **EOF** プロパティがサポートされています。 **BOF**と**EOF**は、**レコードセット**の先頭と末尾に配置される "ファントム" レコードと考えることができます。 **BOF**と**EOF**をカウントすると、サンプル**レコードセット**は次のようになります。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|あなた Bob's 有機理屈 Pears|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle ラウト|45.6000|  
|51|Manjimup 理屈リンゴ|53.0000|  
|74|Longlife Tofu|10.0000|  
|EOF|||  
  
 カーソルが最後のレコードを越えて移動すると、 **EOF** は **True**に設定されます。それ以外の場合、値は **False**です。 同様に、カーソルが最初のレコードの前に移動すると、 **BOF** は **True**に設定されます。それ以外の場合、値は **False**です。 これらのプロパティは、通常、次の JScript コードフラグメントに示すように、データセット内のレコードを列挙するために使用されます。  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 **BOF**と**EOF**の両方が**True**の場合、**レコードセット**オブジェクトは空になります。 新しく開いた、空でない**レコードセット**オブジェクトでは、両方のプロパティが**False**になります。 次の JScript コードフラグメントに示すように、 **BOF** プロパティと **EOF** プロパティを一緒に使用して、 **レコードセット** オブジェクトが空であるかどうかを判断できます。  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 このスキームは、すべての種類のカーソルに対して機能し、基になるプロバイダーからは独立しています。 その**RecordCount**プロパティの値がゼロ (0) であるかどうかをチェックして、**レコードセット**オブジェクトの empを判別しようとする場合は、結果のレコード数の返却をサポートする適切なカーソルとプロバイダーを使用するための予防措置をとる必要があります。  
  
 **レコードセット**オブジェクト内の最後のレコードを削除すると、そのカーソルは不確定状態のままになります。 現在のレコードの位置を変更するには、プロバイダーに応じて、 **BOF** プロパティと **EOF** プロパティを **False** のままにします。 詳細については、「 [Delete メソッドを使用したレコードの削除](./deleting-records-using-the-delete-method.md)」を参照してください。