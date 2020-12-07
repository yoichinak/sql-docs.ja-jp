---
description: 相互運用性
title: 相互運用性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a404ee6de56cbd8b5605eca640fdf0e065f16d79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476614"
---
# <a name="interoperability"></a>相互運用性
*相互運用性* とは、1つのアプリケーションがさまざまな dbms で動作する機能です。 ジェネリックで相互運用可能なアプリケーションを作成する必要があるのは、ODBC の開発につながる主な要因の1つでした。 ただし、相互運用性は、"相互運用不可能" から "完全に相互運用可能" になる単純なパスではありません。 パスには多くの分岐があり、それぞれの機能、速度、コードの複雑さ、および開発時間の間にトレードオフが必要です。  
  
 相互運用可能なアプリケーションを作成するプロセスは、次のいくつかの手順に従います。  
  
1.  アプリケーションで ODBC を使用するかどうかを決定します。  
  
2.  相互運用性のレベルを選択し、そのレベルに対応するために必要なトレードオフを決定します。  
  
3.  相互運用可能なコードを記述し、できるだけ完全にテストします。  
  
 相互運用性は、主にアプリケーションライターのドメインであることに注意してください。 ドライバーは1つの DBMS で動作するように設計されており、定義上、相互運用することはできません。 1つの DBMS で ODBC を正しく実装して公開することによって、相互運用性の役割を果たします。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ODBC が正解ですか?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [相互運用性のレベルの選択](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [ターゲット DBMS とドライバーの決定](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [使用するデータベース機能の検討](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [製品サイクルの長さ](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [相互運用可能なアプリケーションの作成](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [相互運用可能なアプリケーションのテスト](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
