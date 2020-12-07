---
description: Property オブジェクト (ADO)
title: Property オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
author: rothja
ms.author: jroth
ms.openlocfilehash: 7edc57495968cb94dbf8714e3b519acac578775f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989983"
---
# <a name="property-object-ado"></a>Property オブジェクト (ADO)
プロバイダーによって定義される ADO オブジェクトの動的特性を表します。  
  
## <a name="remarks"></a>解説  
 ADO オブジェクトには、組み込みと動的の2種類のプロパティがあります。  
  
 組み込みプロパティは ADO で実装されるプロパティで、構文を使用して、新しいオブジェクトですぐに使用でき `MyObject.Property` ます。 オブジェクトの[プロパティ](./properties-collection-ado.md)コレクションには**プロパティ**オブジェクトとして表示されません。そのため、値を変更することはできますが、その特性を変更することはできません。  
  
 動的プロパティは、基になるデータプロバイダーによって定義され、適切な ADO オブジェクトの **properties** コレクションに表示されます。 たとえば、プロバイダー固有のプロパティは、 [レコードセット](./recordset-object-ado.md) オブジェクトがトランザクションをサポートするか更新するかを示します。 これらの追加のプロパティは、その**レコードセット**オブジェクトの**プロパティ**コレクション内の**プロパティ**オブジェクトとして表示されます。 動的プロパティは、コレクションを通じてのみ、または構文を使用して参照でき `MyObject.Properties(0)` `MyObject.Properties("Name")` ます。  
  
 どちらの種類のプロパティも削除できません。  
  
 動的 **プロパティ** オブジェクトには、次の4つの組み込みプロパティがあります。  
  
-   [Name](./name-property-ado.md)プロパティは、プロパティを識別する文字列です。  
  
-   [Type](./type-property-ado.md)プロパティは、プロパティのデータ型を指定する整数です。  
  
-   [Value](./value-property-ado.md)プロパティは、プロパティ設定を含むバリアントです。 **Value** は、 **プロパティ** オブジェクトの既定のプロパティです。  
  
-   [Attributes](./attributes-property-ado.md)プロパティは、プロバイダー固有のプロパティの特性を示す long 型の値です。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Property オブジェクトのプロパティ、メソッド、およびイベント](./property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Command オブジェクト (ADO)](./command-object-ado.md)   
 [Connection オブジェクト (ADO)](./connection-object-ado.md)   
 [Field オブジェクト](./field-object.md)   
 [Properties コレクション (ADO)](./properties-collection-ado.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)