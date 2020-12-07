---
description: インターフェイスの適合性レベル
title: インターフェイスの準拠レベル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb77ab0e77fc8a811acd956673a4ad4fe8664828
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424624"
---
# <a name="interface-conformance-levels"></a>インターフェイスの適合性レベル
平準化の目的は、ドライバーから使用可能な機能をアプリケーションに通知することです。 関数に基づく平準化方式では、この目標を達成することはできません。 ODBC 3 の場合。*x*は、ドライバーが所有する機能に基づいて分類されます。 機能をサポートするには、関数のサポートを含めることができます。また、記述子フィールド、ステートメント属性、 **SQLGetInfo**によって返される情報型の "Y" 値などをサポートすることもできます。  
  
 インターフェイス準拠の仕様を簡略化するために、ODBC では3つの準拠レベルが定義されています。 特定の準拠レベルを満たすには、ドライバーがその準拠レベルのすべての要件を満たしている必要があります。 指定されたレベルに準拠すると、すべての下位レベルに完全な準拠が示されます。  
  
 準拠レベルは、特定の ODBC 関数の一覧については、常に正しくサポートされるとは限りませんが、次のセクションに記載されているサポートされる機能を指定します。 機能のサポートを提供するために、ドライバーは特定の ODBC 関数 (詳細については、「 [関数の一致](../../../odbc/reference/develop-app/function-conformance.md)」を参照)、特定の属性の設定 ( [属性の準拠](../../../odbc/reference/develop-app/attribute-conformance.md)を参照)、および特定の記述子フィールドの一部またはすべての形式の呼び出しをサポートする必要があります (「 [記述子フィールドの準拠](../../../odbc/reference/develop-app/descriptor-field-conformance.md)」を参照)。  
  
 アプリケーションは、データソースに接続し、SQL_ODBC_INTERFACE_CONFORMANCE オプションを使用して **SQLGetInfo** を呼び出すことによって、ドライバーのインターフェイスの準拠レベルを検出します。  
  
 ドライバーは、完全な準拠を要求するレベルを超える機能を自由に実装できます。 アプリケーションでは、 **Sqlgetfunctions** (存在する odbc 関数を判別するため) と **SQLGetInfo** (他のさまざまな odbc 機能に対してクエリを実行するため) を呼び出すことによって、そのような追加機能を検出します。  
  
 ODBC インターフェイスの準拠レベルには、コア、レベル1、レベル2の3つがあります。  
  
> [!NOTE]
>  これらの準拠レベルには、odbc 2.x の同じ名前の ODBC API 準拠レベルとは異なる要件が*あります。* 特に、ODBC*2.X API の* 準拠レベル1によって暗黙的に示されるすべての機能が、コアインターフェイスの準拠レベルの一部になっています。 その結果、多くの ODBC ドライバーによって、コアレベルのインターフェイスの準拠が報告される場合があります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [コア インターフェイスの適合性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [レベル 1 インターフェイスの適合性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [関数の適合性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [属性の適合性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [記述子フィールドの適合性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
