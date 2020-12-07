---
title: Xml データ型に対する XQuery 関数 |Microsoft Docs
description: Xml データ型に対して使用できる XQuery 関数について説明します。
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, functions
- xml data type [SQL Server], XQuery
- functions [SQL Server], XQuery
ms.assetid: 8df0877d-a03f-4ca9-b84e-908c4bb42b5e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e92148b5a85ced147599eafe09156cf41c47021
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037015"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>xml データ型に対する XQuery 関数
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  このトピックとサブトピックでは、 **xml** データ型に対して XQuery を指定するときに使用できる関数について説明します。 W3C 仕様については、「」を参照してください [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](https://go.microsoft.com/fwlink/?LinkId=4873) 。  
  
 XQuery 関数は名前空間に属し http://www.w3.org/2004/07/xpath-functions ます。 W3C 仕様では、これらの関数を表すために "fn:" という名前空間プレフィックスを使用しています。 この関数を使用するときに、"fn:" 名前空間プレフィックスを明示的に指定する必要はありません。 このため、読みやすくするために、このドキュメントでは、名前空間プレフィックスが一般に使用されていません。  
  
 次の表に、 **xml**データ型に対してサポートされている XQuery 関数を示します。  
  
|カテゴリ|関数名|  
|--------------|-------------------|  
|[数値に対する関数]()|[切り上げ](../xquery/numeric-values-functions-ceiling.md)|  
||[floor](../xquery/numeric-values-functions-floor.md)|  
||[誤差](../xquery/numeric-values-functions-round.md)|  
|[文字列値に使用する XQuery 関数]()|[concat](../xquery/functions-on-string-values-concat.md)|  
||[contains](../xquery/functions-on-string-values-contains.md)|  
||[substring](../xquery/functions-on-string-values-substring.md)|  
||[XQuery&#41;&#40;小文字関数 ](../xquery/functions-on-string-values-lower-case.md)|  
||[string-length](../xquery/functions-on-string-values-string-length.md)|  
||[&#40;XQuery&#41;の大文字関数 ](../xquery/functions-on-string-values-upper-case.md)|  
|ブール値に対する関数|[not](../xquery/functions-on-boolean-values-not-function.md)|  
|[ノードの関数]()|[number](../xquery/functions-on-nodes-number.md)|  
||[ローカル名関数 (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[名前空間 uri 関数 (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[コンテキスト関数]()|[last](../xquery/context-functions-last-xquery.md)|  
||[position](../xquery/context-functions-position-xquery.md)|  
|[シーケンスの関数]()|[empty](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[id 関数 (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[XQuery&#41;&#40;集計関数 ]()|[count](../xquery/aggregate-functions-count.md)|  
||[avg](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[sum](../xquery/aggregate-functions-sum.md)|  
|[コンストラクター関数 &#40;XQuery&#41;](../xquery/constructor-functions-xquery.md)|[コンストラクター関数](../xquery/constructor-functions-xquery.md)|  
|[データ アクセサー関数](../xquery/data-accessor-functions.md)|[string](../xquery/data-accessor-functions-string-xquery.md)|  
||[data](../xquery/data-accessor-functions-data-xquery.md)|  
|[ブール型コンストラクター関数 &#40;XQuery&#41;]()|[true 関数 (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[false 関数 (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[QNames &#40;XQuery&#41;に関連する関数 ](./functions-related-to-qnames-expanded-qname.md)|[展開-QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[ローカル名-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[名前空間-QName からの uri (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[XQuery 拡張関数の SQL Server](./xquery-extension-functions-sql-column.md)|[sql: column () 関数 (XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[sql:variable() 関数 (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>参照  
 [xml データ型メソッド](../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
