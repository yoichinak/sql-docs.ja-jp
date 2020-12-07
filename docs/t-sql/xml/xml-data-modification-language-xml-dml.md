---
description: XML データ変更言語 (XML DML)
title: XML データ変更言語 (XML DML)
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2aaa0b9a37527c10de34e1f1037fe33a8dab3608
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496316"
---
# <a name="xml-data-modification-language-xml-dml"></a>XML データ変更言語 (XML DML)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  XML DML (XML データ変更言語) は、XQuery 言語の拡張言語です。 W3C で定義されているように、XQuery 言語には、データ操作 (DML) の部分がありません。 このトピックで紹介する XML DML および XQuery 言語には、**xml** データ型に対して使用できる完全な機能のクエリおよびデータ変更言語が提供されます。  
  
 XML DML では、XQuery に次のキーワードが追加されました。これらのキーワードでは、大文字と小文字が区別されます。  
  
-   **insert**  
  
-   **delete**  
  
-   **replace value of**  
  
 「[XML データ型と列 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md)」の説明に従って **XML** データ型の変数と列を作成し、それらに XML ドキュメントやフラグメントを割り当てることができます。 このような XML インスタンスを変更または更新するには、次の操作を実行します。  
  
-   **xml** データ型の [modify() メソッド (xml データ型)](../../t-sql/xml/modify-method-xml-data-type.md) を使用します。  
  
-   **modify()** メソッド内に適切な XML DML ステートメントを指定します。  
  
 一部の属性では、挿入や削除、値の変更ができないので注意してください。 次に例を示します。  
  
-   **xml** の型指定の有無にかかわらず、属性には **xmlns**、**xmlns:\*** 、**xml:base** を使用します。  
  
-   型指定された **xml** の場合のみ、属性に **xsi:nil**、および **xsi:type** を使用できます。  
  
 その他の制限には、次のようなものがあります。  
  
-   **xml** の型指定の有無にかかわらず、**xml:base** 属性を挿入すると、エラーになります。  
  
-   型指定された **xml** の場合、**xsi:nil** 属性を削除または変更すると、エラーになります。 型指定されていない **xml** の場合は、この属性を削除したり、変更したりすることができます。  
  
-   型指定された **xml** の場合、**xs:type** 属性の値を変更すると、エラーになります。 型指定されていない **xml** の場合は、この属性の値を変更できます。  
  
 型指定された xml インスタンスを変更する場合、最終的な形式が、その型の有効なインスタンスである必要があります。 そうでない場合は、検証エラーが返されます。  
  
## <a name="see-also"></a>参照  
 [insert &#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md)   
 [delete &#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md)   
 [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML データのインスタンスの作成](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)  
  
  
