---
description: メタデータの使用方法
title: メタデータの使用方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca61677b0001ba4c39f81f80f6e3cbce26f27910
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476634"
---
# <a name="how-is-metadata-used"></a>メタデータの使用方法
アプリケーションは、ほとんどの結果セット操作にメタデータを必要とします。 たとえば、列のデータ型を使用して、列にバインドされている変数の種類を判断します。 文字型の列のバイト長を使用して、その列のデータを表示するために必要な領域の量を決定します。 アプリケーションが列のメタデータを判断する方法は、アプリケーションの種類によって異なります。  
  
 縦向きのアプリケーションは、定義済みのテーブルを処理し、これらのテーブルに対して定義済みの操作を実行します。 アプリケーションが記述され、アプリケーション開発者によって制御される前に、このようなアプリケーションの結果セットのメタデータが定義されているため、アプリケーションにハードコーディングすることができます。 たとえば、データ ソース内で受注 ID 列が 4 バイト integer 型で定義されている場合、アプリケーションは常に 4 バイト integer をこの列にバインドできます。 メタデータがアプリケーション内でハードコーディングされている場合、アプリケーションが使用するテーブルへの変更は、通常、アプリケーション コードに対する変更になります。 このような変更は通常、アプリケーションの新しいリリースの一部として行われるため、これはほとんど問題にはなりません。  
  
 垂直アプリケーションと同様に、カスタムアプリケーションは通常、定義済みのテーブルを操作し、それらのテーブルに対して定義済みの操作を実行します。 たとえば、3つの異なるデータソース間でデータを転送するようにアプリケーションを作成することができます。転送されるデータは、通常、アプリケーションの作成時に知られます。 したがって、カスタムアプリケーションでは、ハードコーディングされたメタデータが必要になる傾向もあります。  
  
 汎用アプリケーション (特にアドホッククエリをサポートするアプリケーション) では、作成される結果セットのメタデータはほとんど知られていません。 そのため、実行時にメタデータを検出するには、 **Sqlnumresultcols**、 **SQLDescribeCol**、および **sqlcolattribute**関数を使用します。これについては、次のセクション「 [SQLDescribeCol と sqlcolattribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)」で説明します。  
  
 すべてのアプリケーションは、種類に関係なく、カタログ関数によって返される結果セットのメタデータをハードコーディングできます。 これらの結果セットは、このマニュアルの「参照」セクションで定義されています。
