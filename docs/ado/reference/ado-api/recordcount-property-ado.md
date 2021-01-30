---
description: RecordCount プロパティ (ADO)
title: RecordCount プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
author: rothja
ms.author: jroth
ms.openlocfilehash: 76f3911ccc240a29829efcd5aa301ff5dfb8cbd5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170454"
---
# <a name="recordcount-property-ado"></a>RecordCount プロパティ (ADO)

[レコードセット](./recordset-object-ado.md)オブジェクト内のレコードの数を示します。
  
## <a name="return-value"></a>戻り値

**レコードセット** 内のレコードの数を示す **Long 型** の値を返します。
  
## <a name="remarks"></a>コメント

レコード **セット** オブジェクト内のレコードの数を調べるには、 **RecordCount** プロパティを使用します。 ADO がレコードの数を特定できない場合、またはプロバイダーまたはカーソルの種類が **RecordCount** をサポートしていない場合、プロパティは-1 を返します。 閉じた **レコードセット** の **RecordCount** プロパティを読み取ると、エラーが発生します。

#### <a name="bookmarks-or-approximate-positioning"></a>ブックマークまたはおおよその配置

Recordset オブジェクトがブックマークまたはおおよその配置をサポートしている場合、この *プロパティはレコード* セット内のレコードの正確な数を返します。 このプロパティは、レコードセットが完全に設定されているかどうかに関係なく、正確な数値を返します。

これに対し、レコードセットオブジェクトがブックマークまたはおおよその配置をサポートし *てい* ない場合、このプロパティにアクセスするとリソースが大幅に消費される可能性があります。 ドレインは、すべてのレコードを取得して、正確な RecordCount 値を返す必要があるために発生します。

- ブックマークに関連する **Adbookmark** 。
- **Adapproxposition** は、おおよその配置に関連します。

> [!NOTE]
> ADO バージョン2.8 以前では、サーバー側カーソルが使用されている場合、SQLOLEDB プロバイダーはすべてのレコードをフェッチします。これは、**サポート (adApproxPosition)** と **サポート (adbookmark)** の両方に対して **True** が返されるという事実です。
  
レコード **セット** オブジェクトのカーソルの種類は、レコード数を決定できるかどうかに影響します。 **RecordCount** プロパティは、順方向専用カーソルの場合は-1 を返します。静的カーソルまたはキーセットカーソルの実際の数。データソースに応じて、-1 または動的カーソルの実際の数のいずれかです。
  
## <a name="applies-to"></a>適用対象

[Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照

[Filter プロパティと RecordCount プロパティの例 (VB)](./filter-and-recordcount-properties-example-vb.md)   
[Filter プロパティと RecordCount プロパティの例 (VC + +)](./filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition プロパティ (ADO)](./absoluteposition-property-ado.md)   
[PageCount プロパティ (ADO)](./pagecount-property-ado.md)