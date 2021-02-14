---
title: XQuery プロローグ |Microsoft Docs
description: クエリ処理に必要な環境を作成する一連の宣言と定義を含む XQuery プロローグについて説明します。
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
- namespaces [XQuery]
- default namespace declarations
ms.assetid: 03924684-c5fd-44dc-8d73-c6ab90f5e069
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b460f6da448e45d688ebcc08f418a9acbae85b8
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341845"
---
# <a name="modules-and-prologs---xquery-prolog"></a>モジュールとプロローグ - XQuery プロローグ
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  XQuery クエリは、プロローグ (序文) と本文で構成されます。 XQuery プロローグは、クエリ処理に必要な環境を作成する一連の宣言と定義です。 SQL Server では、XQuery プロローグに名前空間の宣言を含めることができます。 XQuery 本文は、目的のクエリ結果を指定する一連の式で構成されます。  
  
 たとえば、次の XQuery は、製造手順を XML として格納する **xml** 型の命令列に対して指定されています。 このクエリでは、ワーク センターの場所 `10` に関する製造手順が取得されます。 `query()` **Xml** データ型のメソッドは、XQuery を指定するために使用されます。  
  
```  
SELECT Instructions.query('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') AS Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   XQuery プロローグには、名前空間プレフィックス (AWMI) の宣言が含まれてい `(namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";` ます。  
  
-   `declare namespace` キーワードは、クエリ本文で後から使用される名前空間プレフィックスを定義します。  
  
-   `/AWMI:root/AWMI:Location[@LocationID="10"]` がクエリの本文です。  
  
## <a name="namespace-declarations"></a>名前空間の宣言  
 次のクエリで示すように、名前空間の宣言でプレフィックスを定義し、名前空間 URI に関連付けます。 クエリでは、 `CatalogDescription` は **xml** 型の列です。  
  
 この列に対する XQuery の指定では、クエリのプロローグで `declare namespace` 宣言を指定して、製品説明のプレフィックス `PD` を名前空間 URI に関連付けています。 このプレフィックスは、名前空間 URI ではなく、クエリ本文で使用されます。 結果の XML 内のノードは、名前空間 URI に関連付けられている名前空間にあります。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 クエリの読みやすさを向上させるには、を使用してクエリプロローグでプレフィックスと名前空間のバインドを宣言する代わりに、WITH XMLNAMESPACES を使用して名前空間を宣言し `declare namespace` ます。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
  
SELECT CatalogDescription.query('  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 詳細については、「 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)」を参照してください。  
  
### <a name="default-namespace-declaration"></a>既定の名前空間の宣言  
 宣言を使用して名前空間プレフィックスを宣言する代わりに、宣言を使用して、 `declare namespace` `declare default element namespace` 要素名の既定の名前空間をバインドできます。 この場合、プレフィックスを指定する必要はありません。  
  
 次の例では、クエリ本文のパス式に名前空間プレフィックスが指定されていません。 既定では、すべての要素名は、プロローグに指定された既定の名前空間に属します。  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace  "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
 WITH XMLNAMESPACES を使用して、既定の名前空間を宣言できます。  
  
```  
WITH XMLNAMESPACES (DEFAULT 'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription')  
SELECT CatalogDescription.query('  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
## <a name="see-also"></a>参照  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)  
  
  
