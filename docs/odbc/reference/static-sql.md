---
description: 静的 SQL
title: 静的 SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19c4ec3454a5d5891a87203fe8c7aeaff21b239b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428984"
---
# <a name="static-sql"></a>静的 SQL
Embedded sql の [例](../../odbc/reference/embedded-sql-example.md) に示されている embedded sql は、静的 sql と呼ばれています。 これは、プログラム内の SQL ステートメントが静的であるため、静的 SQL と呼ばれます。つまり、プログラムが実行されるたびに変更されることはありません。 前のセクションで説明したように、これらのステートメントは、プログラムの残りの部分がコンパイルされるときにコンパイルされます。  
  
 静的 SQL は多くの状況で適切に動作し、プログラムのデザイン時にデータアクセスを決定できる任意のアプリケーションで使用できます。 たとえば、注文入力プログラムは、常に同じステートメントを使用して新しい注文を挿入し、航空会社の予約システムは常に同じステートメントを使用して、座席の状態を [使用可能] から [予約済み] に変更します。 これらの各ステートメントは、ホスト変数を使用して一般化されます。販売注文には異なる値を挿入できます。また、別の座席を予約することもできます。 このようなステートメントはプログラムにハードコーディングされる可能性があるため、このようなプログラムでは、コンパイル時にステートメントを解析、検証、最適化する必要があるという利点があります。 これにより、比較的高速なコードが生成されます。
