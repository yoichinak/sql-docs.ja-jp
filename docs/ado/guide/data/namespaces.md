---
description: 名前空間
title: 名前空間 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: rothja
ms.author: jroth
ms.openlocfilehash: 03d70d1e5df026e13e23c9759462f53114f4d2af
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980263"
---
# <a name="namespaces"></a>名前空間
ADO の XML 永続化形式では、次の4つの名前空間が使用されます。  
  
## <a name="remarks"></a>解説  
 ADO の XML 永続化形式では、次の4つの名前空間が使用されます。  
  
|Prefix|説明|  
|------------|-----------------|  
|s|現在のレコードセットのスキーマを定義する要素と属性を含む "XML-Data" 名前空間を参照します。|  
|dt|データ型定義の指定を参照します。|  
|rs|ADO レコードセットのプロパティと属性に固有の要素および属性を含む名前空間を参照します。|  
|z|現在の行セットのスキーマを参照します。|  
  
 クライアントは、仕様で定義されているように、これらの名前空間に独自のタグを追加しないでください。 たとえば、クライアントは名前空間を "urn: schema-MyOwnTag: rowset" として定義してから、"rs:" のようなものを書き出す必要があります。 名前空間の詳細については、「 [XML 勧告の W3C 名前空間](http://www.w3.org/TR/REC-xml-names/)」を参照してください。  
  
> [!IMPORTANT]
>  スキーマタグの ID は "RowsetSchema" である必要があります。また、現在の行セットのスキーマを参照するために使用される名前空間は、"#RowsetSchema" を指している必要があります。  
  
 名前空間のプレフィックス (コロンと等号の間の部分) は任意です。  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 この名前が XML ドキュメント全体で一貫して使用されている限り、ユーザーはこれを任意の名前に定義できます。 ADO は常に "s"、"rs"、"dt"、"z" を書き込みますが、これらのプレフィックス名は読み込みコンポーネントにハードコードされません。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](./persisting-records-in-xml-format.md)