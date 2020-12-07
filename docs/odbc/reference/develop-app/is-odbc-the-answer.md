---
description: ODBC が正解ですか?
title: ODBC が正解ですか? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a51c4248a041d65f00ec1846f60788cded68f7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476604"
---
# <a name="is-odbc-the-answer"></a>ODBC が正解ですか?
相互運用性の問題を調査する前に、アプリケーションで ODBC を使用するかどうかを検討してください。 これは、ODBC のガイドで質問されることもありますが、実際には正当な質問です。 ODBC はネイティブデータベース Api を完全に置き換えるように設計されていません。また、すべての状況でデータベースアクセスを提供するように設計されていませんでした。 これは、データベースに共通のインターフェイスを提供するように設計されており、アプリケーションプログラマが複数のデータベースへのリンクについて学習し、維持する必要がないようにするためのものです。  
  
 カスタムアプリケーションは、ネイティブデータベース Api の有力な候補です。 主な理由は、カスタムアプリケーションが1つの DBMS で動作し、相互運用可能である必要がないことです。 ネイティブデータベース Api は、特定の DBMS の機能を公開する ODBC よりも優れたジョブを実行し、ODBC によって公開されていない機能を公開する可能性があります。 さらに、カスタムアプリケーションの開発者は、通常、DBMS のネイティブデータベース API に精通しているため、ODBC を学習する理由はほとんどありません。 ただし、一部の Dbms では ODBC がネイティブデータベース API であることに注意してください。  
  
 ODBC の候補となるのはどのアプリケーションか。 最適な候補は、複数の DBMS で動作するアプリケーションです。 これには、ほぼすべての汎用アプリケーションと垂直アプリケーションが含まれます。 また、さまざまなカスタムアプリケーションも含まれています。 たとえば、いくつかの異なる Dbms を使用するカスタムアプリケーションは、複数のネイティブ Api を使用する場合よりも ODBC で簡単に記述できます。 また、ODBC を使用して作成されたカスタムアプリケーションは、企業が DBMS 間を移動したり、異なる Dbms に対して同じアプリケーションを配置したりすると、より簡単に移行できます。
