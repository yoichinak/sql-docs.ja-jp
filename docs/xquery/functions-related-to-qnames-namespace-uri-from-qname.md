---
title: 名前空間-QName からの uri (XQuery) |Microsoft Docs
description: 名前空間 uri from QName 関数を使用して、QName の名前空間 URI を取得する方法について説明します。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 035b92b719431b5a9b74f951f20d51911a41d59c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035780"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>QNames に関係する関数 - namespace-uri-from-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg*によって指定された QName の名前空間 uri を表す文字列を返します。 *$Arg*が空のシーケンスの場合、結果は空のシーケンスになります。  
  
## <a name="syntax"></a>構文  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 は、名前空間 URI が返される QName です。  
  
## <a name="examples"></a>例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. QName から名前空間 URI を取得する  
 実際のサンプルについては、「 [ローカル名-QName からの &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md)」を参照してください。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **名前空間 uri From QName ()** 関数は、Xs: anyURI ではなく xs: string のインスタンスを返します。  
  
## <a name="see-also"></a>参照  
 [QNames &#40;XQuery&#41;に関連する関数 ](./functions-related-to-qnames-expanded-qname.md)  
  
