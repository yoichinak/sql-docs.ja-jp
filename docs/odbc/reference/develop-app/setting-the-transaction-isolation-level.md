---
description: トランザクション分離レベルの設定
title: トランザクション分離レベルを設定する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f871ef9e25cb5745987079a4d94272d2f430dfaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476414"
---
# <a name="setting-the-transaction-isolation-level"></a>トランザクション分離レベルの設定
トランザクション分離レベルを設定するには、アプリケーションで SQL_ATTR_TXN_ISOLATION 接続属性を使用します。 データソースが要求された分離レベルをサポートしていない場合、ドライバーまたはデータソースはより高いレベルを設定できます。 データソースがサポートするトランザクション分離レベルと既定の分離レベルを決定するために、アプリケーションでは、SQL_TXN_ISOLATION_OPTION オプションと SQL_DEFAULT_TXN_ISOLATION オプションを使用して **SQLGetInfo** を呼び出します。  
  
 トランザクションの分離レベルが高いほど、データベースデータの整合性を最大限に保護できます。 シリアル化可能なトランザクションは、他のトランザクションの影響を受けないことが保証されるため、データベースの整合性を維持することが保証されます。  
  
 ただし、トランザクションの分離レベルが高いほど、パフォーマンスが低下する可能性があります。これは、アプリケーションがデータのロックが解放されるまで待機する必要が生じる可能性が高くなるためです。 アプリケーションでは、次の場合にパフォーマンスを向上させるために、下位レベルの分離を指定できます。  
  
-   アプリケーションのトランザクションに干渉する可能性がある他のトランザクションが存在しないことを保証できる場合。 この状況は、限られた状況でのみ発生します。たとえば、小規模企業の1人が、個人データを含む dBASE ファイルを1台のコンピューターに保持していて、これらのファイルを共有していない場合などです。  
  
-   速度が精度よりも重要であり、エラーが小さいと思われる場合。 たとえば、企業では小さな売上が多く、大きな売上はめったにないとします。 開いているすべての販売の合計値を推定するトランザクションでは、Read 未確定分離レベルが安全に使用される可能性があります。 トランザクションには、開いている注文や閉じられた注文が含まれ、その後ロールバックされますが、通常、これらの順序はキャンセルされます。このような注文が発生するたびにブロックされることはないため、トランザクションははるかに高速になります。  
  
 詳細については、「 [オプティミスティック同時実行制御](../../../odbc/reference/develop-app/optimistic-concurrency.md)」を参照してください。
