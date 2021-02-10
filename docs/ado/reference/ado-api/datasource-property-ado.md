---
description: DataSource プロパティ (ADO)
title: DataSource プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
author: rothja
ms.author: jroth
ms.openlocfilehash: 73058aa92e594528ef214a9ffa93fa0f58d29b76
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100025669"
---
# <a name="datasource-property-ado"></a>DataSource プロパティ (ADO)
[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトとして表されるデータを格納するオブジェクトを示します。  
  
## <a name="remarks"></a>解説  
 このプロパティは、データ環境を使用してデータバインドコントロールを作成するために使用されます。 データ環境では、 **レコードセット** オブジェクトとして表される名前付きオブジェクト (データメンバー) を含むデータ (データソース) のコレクションを保持します。  
  
 [DataMember](../../../ado/reference/ado-api/datamember-property.md)プロパティと **DataSource** プロパティは、組み合わせて使用する必要があります。  
  
 参照されるオブジェクトは、 **IDataSource** インターフェイスを実装する必要があり、 **IRowset** インターフェイスを含んでいる必要があります。  
  
## <a name="usage"></a>使用法  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [DataMember プロパティ](../../../ado/reference/ado-api/datamember-property.md)
