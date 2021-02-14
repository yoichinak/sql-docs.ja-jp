---
title: パス式での省略構文の使用 |Microsoft Docs
description: XQuery パス式での省略構文の使用方法について説明します。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
author: rothja
ms.author: jroth
ms.openlocfilehash: 959d5498011984fc1f400567517d3b5b07727fcc
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100339929"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>パス式 - 省略構文の使用
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  [XQuery のパス式を理解](../xquery/path-expressions-xquery.md)するすべての例では、パス式の省略構文を使用します。 パス式の軸ステップの省略構文では、軸名とノード テストを 2 つのコロン (::) で区切り、その後にステップ修飾子を指定します。ステップ修飾子は、指定しなくてもかまいません。  
  
 次に例を示します。  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery は、パス式で次の省略をサポートしています。  
  
-   **子** 軸は既定の軸です。 したがって、式のステップでは、 **child::** axis を省略できます。 たとえば、は `/child::ProductDescription/child::Summary` として書き込むことができ `/ProductDescription/Summary` ます。  
  
-   **属性** 軸はとして省略でき @ ます。 たとえば、は `/child::ProductDescription[attribute::ProductModelID=10]` として書き込むことができ `/ProudctDescription[@ProductModelID=10]` ます。  
  
-   **/Descendant-or-self:: node ()/** は//のように省略できます。 たとえば、は `/descendant-or-self::node()/child::act:telephoneNumber` として書き込むことができ `//act:telephoneNumber` ます。  
  
     上記のクエリは、Contact テーブルの AdditionalContactInfo 列に格納されているすべての電話番号を取得します。 AdditionalContactInfo のスキーマは、 \<telephoneNumber> 要素がドキュメント内の任意の場所に表示されるように定義されています。 したがって、すべての電話番号を取得するには、ドキュメント内のすべてのノードを検索する必要があります。 検索は、ドキュメントのルートから開始され、続いてすべての子孫ノードが検索されます。  
  
     次のクエリは、特定の顧客の連絡先のすべての電話番号を取得します。  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="https://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     パス式を省略構文に置き換えると `//act:telephoneNumber` 、同じ結果が得られます。  
  
-   ステップの **self:: node ()** は、1つのドット (.) に省略できます。 ただし、ドットは、 **自己:: node ()** と同等ではないか、交換できません。  
  
     たとえば、次のクエリでは、ドットを使用して、ノードではなく値を表しています。  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   ステップの **parent:: node ()** は、二重のドット (..) に省略できます。  
  
  
