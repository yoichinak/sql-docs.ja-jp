---
description: 結果セットのメタデータ
title: 結果セットのメタデータ |Microsoft Docs
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
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46738682900509d22df1eebaa22b13d3abfb729e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424594"
---
# <a name="result-set-metadata"></a>結果セットのメタデータ
*メタ* データは、他のデータを記述するデータです。 たとえば、結果セットのメタデータには、結果セット内の列数、列のデータ型、名前、有効桁数、null 値の許容属性などの結果セットが記述されます。  
  
 相互運用可能なアプリケーションでは、常に結果セットの列のメタデータを確認する必要があります。 結果セット内の列のメタデータは、カタログ関数によって返される列のメタデータとは異なる場合があります。 たとえば、2つのテーブルを結合して作成された結果セットに更新可能な列が含まれているとします。 **Sqlcolumnprivileges**はユーザーが列を更新できることを示している場合がありますが、列が結合の "多" 側にある場合、結果セットのメタデータが返されないことがあります。多くのデータソースでは、"多" 側ではなく、結合の "一" 側の列を更新できます。 データソースでは、結果セットの作成中にデータ型が昇格される可能性があるので、データ型が同じであると見なすことはできません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [メタデータの使用方法](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol および SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
