---
description: カタログの位置
title: カタログの位置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 513c2449d296d167c499942636cbb94d637a2ede
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465964"
---
# <a name="catalog-position"></a>カタログの位置
識別子に含まれるカタログ名の位置と、識別子の残りの部分との分離方法は、データソースとデータソースによって異なります。 たとえば、Xbase データソースでは、カタログ名はディレクトリであり、Microsoft® Windows®では、テーブル名 (ファイル名) から円記号 () で区切られ \\ ます。 次の図は、この条件を示しています。  
  
 ![カタログの位置: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 SQL Server データソースでは、カタログはデータベースで、スキーマ名とテーブル名はピリオド (.) で区切られます。  
  
 ![カタログの位置: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Oracle データソースでは、カタログはデータベースでもありますが、テーブル名に従います。スキーマ名とテーブル名は、アットマーク (@) で区切られます。  
  
 ![カタログの位置: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 アプリケーションでは、カタログの区切り記号とカタログ名の場所を決定するために、SQL_CATALOG_NAME_SEPARATOR オプションと SQL_CATALOG_LOCATION オプションを使用して **SQLGetInfo** を呼び出します。 相互運用可能なアプリケーションでは、これらの値に基づいて識別子を構築する必要があります。  
  
 複数の部分を含む識別子を引用符で囲む場合、アプリケーションでは、各部分を個別に引用符で囲む必要があり、識別子を区切る文字を引用符で囲む必要はありません。 たとえば、次のステートメントでは、Xbase テーブルのすべての行と列を選択して、カタログ (\XBASE\SALES\CORP) 名とテーブル (Parts) 名を引用符で囲んでいます。ただし、カタログ区切り記号 () は使用しません \\ 。  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 次のステートメントでは、Oracle テーブルのすべての行と列を選択して、カタログ (Sales)、スキーマ (企業)、およびテーブル (部分) の名前を引用します。ただし、カタログ (@) またはスキーマ (.) の区切り記号は指定できません。  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 識別子の引用符の詳細については、次の「 [引用符で囲ま](../../../odbc/reference/develop-app/quoted-identifiers.md)れた識別子」を参照してください。
