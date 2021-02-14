---
title: データアクセサー関数 |Microsoft Docs
description: 'XQuery のデータアクセサー関数 fn: data ()、fn: string ()、text () を使用する方法について説明します。'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
author: rothja
ms.author: jroth
ms.openlocfilehash: 53ce941c88e2ab551ac0787126e2cf981d353819
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100351068"
---
# <a name="data-accessor-functions"></a>データ アクセサー関数
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  このセクションのトピックでは、データアクセサー関数のサンプルコードについて説明します。  
  
## <a name="understanding-fndata-fnstring-and-text"></a>fn:data()、fn:string()、text() について  
 XQuery には、スカラー値を抽出するための関数 **fn: data ()** 、ノードからの型指定された値、テキストノードを返すノードテスト **テキスト (** )、およびノードの文字列値を返す関数 **fn: string ()** があります。 この 3 つのアクセサーの使用方法が紛らわしい場合があります。 次に、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] でこれらを使用する場合のガイドラインを示します。 XML インスタンス \<age> 12 \</age> は、図を示す目的で使用されます。  
  
-   型指定されていない XML: パス式/age/text () は、テキストノード "12" を返します。 関数 fn: data (/age) は文字列値 "12" を返します。したがって、fn: string (/age) が返されます。  
  
-   型指定された XML: 式/age/text () は、単純型の要素に対して静的エラーを返し \<age> ます。 一方、fn: data (/age) は整数12を返します。 fn:string(/age) は文字列 "12" を返します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [string 関数 &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [データ関数 &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>参照  
 [パス式 &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
