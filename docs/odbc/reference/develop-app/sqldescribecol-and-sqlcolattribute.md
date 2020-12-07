---
description: SQLDescribeCol および SQLColAttribute
title: SQLDescribeCol および SQLColAttribute |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de375ea207e8e393fa36c9795ebf0e3ca5f428b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424504"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol および SQLColAttribute
**SQLDescribeCol** および **sqlcolattribute** は、結果セットのメタデータを取得するために使用されます。 これら2つの関数の違いは、 **SQLDescribeCol** は常に同じ5つの情報 (列の名前、データ型、有効桁数、小数点以下桁数、および null 値の許容属性) を返すことです。 **sqlcolattribute** は、アプリケーションによって要求された1つの情報を返します。 ただし、 **Sqlcolattribute** は、列の大文字と小文字の区別、表示サイズ、更新性、および検索性など、より高度なメタデータの選択を返すことができます。  
  
 多くのアプリケーション (特に、データのみを表示するアプリケーション) では、 **SQLDescribeCol**によって返されるメタデータのみが必要です。 これらのアプリケーションでは、情報が1回の呼び出しで返されるため、 **Sqlcolattribute**よりも**SQLDescribeCol**を使用する方が高速です。 他のアプリケーション (特にデータを更新するアプリケーション) では、 **Sqlcolattribute** によって返される追加のメタデータが必要であるため、両方の関数を使用します。 また、 **Sqlcolattribute** はドライバー固有のメタデータをサポートしています。詳細については、「 [ドライバー固有のデータ型、記述子の型、情報の種類、診断の種類、および属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)」を参照してください。  
  
 アプリケーションでは、ステートメントが準備または実行された後、および結果セットのカーソルが閉じられる前に、いつでも結果セットのメタデータを取得できます。 ステートメントを準備して実行する前に、結果セットのメタデータを必要とするアプリケーションはほとんどありません。 可能な場合は、ステートメントが実行されるまで、アプリケーションはメタデータの取得を待機する必要があります。これは、一部のデータソースでは、準備されたステートメントのメタデータを返すことができないため、ドライバーでこの機能をエミュレートすることは多くの場合、低速のプロセスです。 たとえば、ドライバーでは、 **SELECT**ステートメントの**where**句を、 **1 = 2**で、結果のステートメントを実行する句で置き換えることによって、0行の結果セットを生成する場合があります。  
  
 メタデータは、多くの場合、データソースから取得するとコストがかかります。 このため、ドライバーはサーバーから取得したすべてのメタデータをキャッシュし、結果セット上のカーソルが開いている間は、それを保持する必要があります。 また、アプリケーションは、絶対に必要なメタデータのみを要求する必要があります。
