---
description: Property オブジェクト (ADOX)
title: Property オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
author: rothja
ms.author: jroth
ms.openlocfilehash: 3b2cfa49dcab6c3bc3b56ab5f2d987c026fa3f85
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983463"
---
# <a name="property-object-adox"></a>Property オブジェクト (ADOX)
ADOX オブジェクトの特性を表します。  
  
## <a name="remarks"></a>解説  
 ADOX オブジェクトには、組み込みと動的の2種類のプロパティがあります。  
  
 組み込みプロパティは、新しいオブジェクトですぐに使用できるプロパティで、MyObject 構文を使用します。 オブジェクトの [プロパティコレクション](../ado-api/properties-collection-ado.md)にはプロパティオブジェクトとして表示されません。そのため、値を変更することはできますが、その特性を変更することはできません。  
  
 動的プロパティは、基になるデータプロバイダーによって定義され、適切な ADOX オブジェクトの Properties コレクションに表示されます。  動的プロパティを参照できるのは、コレクションを介して、MyObject (0) または MyObject. Properties ("Name") 構文を使用する場合のみです。  
  
 どちらの種類のプロパティも削除できません。  
  
 動的プロパティオブジェクトには、次の4つの組み込みプロパティがあります。  
  
 [Name](../ado-api/name-property-ado.md)プロパティは、プロパティを識別する文字列です。  
  
 [Type](../ado-api/type-property-ado.md)プロパティは、プロパティのデータ型を指定する整数です。  
  
 [Value](../ado-api/value-property-ado.md)プロパティは、プロパティ設定を含むバリアントです。 Value は、プロパティオブジェクトの既定のプロパティです。  
  
 [Attributes](../ado-api/attributes-property-ado.md)プロパティは、プロバイダー固有のプロパティの特性を示す long 型の値です。  
  
 ここでは、次のトピックについて説明します。  
  
-   [ADOX Property オブジェクトのプロパティ、メソッド、およびイベント](./adox-property-object-properties-methods-and-events.md)