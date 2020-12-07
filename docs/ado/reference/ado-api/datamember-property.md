---
description: DataMember プロパティ
title: DataMember プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
author: rothja
ms.author: jroth
ms.openlocfilehash: 034afc971021f6bcfa4db7877d0409aeb817fc6f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974273"
---
# <a name="datamember-property"></a>DataMember プロパティ
[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)プロパティによって参照される[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)から取得されるデータメンバーの名前を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **文字列**値を設定または返します。 名前の大文字と小文字は区別されません。  
  
## <a name="remarks"></a>解説  
 このプロパティは、データ環境を使用してデータバインドコントロールを作成するために使用されます。 データ環境では、 [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md) オブジェクトとして表される名前付きオブジェクト (データメンバー) を含むデータ (データソース) のコレクションを保持します。  
  
 **DataMember**プロパティと**DataSource**プロパティを一緒に使用する必要があります。  
  
 **DataMember**プロパティは、 **DataSource**プロパティによって指定されたオブジェクトを**レコードセット**オブジェクトとして表現します。 このプロパティを設定する前に、 **レコードセット** オブジェクトを閉じる必要があります。 **Datasource**プロパティの前に**datamember**プロパティが設定されていない場合、または**datasource**プロパティで指定されたオブジェクトによって**datamember**名が認識されない場合は、エラーが生成されます。  
  
## <a name="usage"></a>使用法  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [DataSource プロパティ (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
