---
description: 相互運用可能なアプリケーションのテスト
title: 相互運用可能なアプリケーションのテスト |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: feebbe5914e9da1e414f5c77a1a69bc0a6e0e7b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487525"
---
# <a name="testing-interoperable-applications"></a>相互運用可能なアプリケーションのテスト
相互運用可能なアプリケーションのテストは、時間がかかり、市場に新しいドライバーが継続的に表示されるため、ほとんどの場合は不可能です。 ただし、妥当なレベルのテストが可能です。 相互運用性が制限されているか、または低いアプリケーションは、サポートが保証されているドライバーに対してのみテストする必要があります。 ただし、これらのドライバーに対して完全にテストする必要があります。  
  
 高度に相互運用可能なアプリケーションは、すべてのドライバーに対して実際にテストすることはできません。 ほとんどのアプリケーション開発者は、少数のドライバーと cursorily に対して完全にテストし、さらに多くのことを行うことをお勧めします。 テスト対象のドライバーには、アプリケーションの市場で最も人気のある Dbms に最も人気のあるドライバーが含まれている必要があります。市場ですべての Dbms が対象となっている場合は、デスクトップとサーバーの両方の Dbms のドライバーをテストする必要があります。  
  
 ODBC アプリケーションのテストにおける問題の1つは、アプリケーション自体、ドライバーマネージャー、ドライバー、DBMS、および場合によってはネットワークソフトウェアまたはゲートウェイに関連するコンポーネントの数です。 アプリケーションを使用すると、ODBC 関数によって返されたエラーメッセージを **SQLGetDiagField** および **SQLGetDiagRec**を介して送信することにより、エラーを追跡しやすくなります。 これらのメッセージは、エラーが発生した製造元とコンポーネントを識別します。 詳細については、「 [診断](../../../odbc/reference/develop-app/diagnostics.md)」を参照してください。
