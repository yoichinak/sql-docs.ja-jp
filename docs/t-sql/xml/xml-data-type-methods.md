---
description: xml データ型のメソッド
title: xml データ型のメソッド
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b139187edc98242b7b4efc03ebd53a71fe415f3
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116563"
---
# <a name="xml-data-type-methods"></a>xml データ型のメソッド
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **xml** データ型メソッドを使用すると、**xml** 型の変数または列に格納されている XML インスタンスに対してクエリを実行できます。 このセクションのトピックでは、**xml** データ型メソッドの使用方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[query&#40;&#41; メソッド &#40;xml データ型&#41;](../../t-sql/xml/query-method-xml-data-type.md)|query() メソッドを使用して XML インスタンスに対してクエリを実行する方法について説明します。|  
|[value&#40;&#41; メソッド &#40;xml データ型&#41;](../../t-sql/xml/value-method-xml-data-type.md)|value() メソッドを使用して XML インスタンスから SQL 型の値を取得する方法について説明します。|  
|[exist&#40;&#41; メソッド &#40;xml データ型&#41;](../../t-sql/xml/exist-method-xml-data-type.md)|exist() メソッドを使用して、クエリから空でない結果が返されるかどうかを判断する方法について説明します。|  
|[modify&#40;&#41; メソッド &#40;xml データ型&#41;](../../t-sql/xml/modify-method-xml-data-type.md)|modify() メソッドを使用して、[XML データ変更言語 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md) のステートメントを指定し、更新を行う方法について説明します。|  
|[nodes&#40;&#41; Method &#40;xml データ型&#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|nodes() メソッドを使用して、XML を複数行に細分化し、XML ドキュメントの各部分をそれぞれ行セットに反映する方法について説明します。|  
|[XML データ内部のリレーショナル データのバインド](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|XML 内部の XML 以外のデータをバインドする方法について説明します。|  
|[xml データ型メソッドの使用に関するガイドライン](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|**xml** データ型メソッドの使用に関するガイドラインを示します。|  
  
 これらのメソッドは、ユーザー定義型メソッドの呼び出し構文を使用して呼び出します。 次に例を示します。  
  
```sql
SELECT XmlCol.query(' ... ')  
FROM Table  
```  
  
> [!NOTE]  
>  **xml** データ型のメソッドである **query()** 、**value()** 、および **exist()** は、NULL の XML インスタンスに対して実行された場合 NULL を返します。 また、**modify()** は何も返しませんが、**nodes()** は NULL 入力以外の場合は行セットを、NULL 入力の場合は空の行セットを返します。  
  
## <a name="see-also"></a>参照  
 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML データのインスタンスの作成](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
