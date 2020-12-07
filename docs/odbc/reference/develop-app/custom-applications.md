---
description: カスタム アプリケーション
title: カスタムアプリケーション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56829c72264ba128554af0534e8a6bfa16254142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429394"
---
# <a name="custom-applications"></a>カスタム アプリケーション
カスタムアプリケーションは、通常、いくつかの Dbms に対して特定のタスクを実行します。 たとえば、アプリケーションが1つの DBMS からデータを取得してレポートを生成したり、複数の Dbms 間でデータを転送したりすることがあります。 これらのアプリケーションの共通点は、アプリケーションが記述される前にこれらの Dbms が知られており、アプリケーションの実行中に変更される可能性が低いことです。  
  
 したがって、カスタムアプリケーションでは、ほとんどまたはまったく相互運用性は必要ありません。 アプリケーション開発者は、DBMS ごとに1つのドライバーを選択し、それらのドライバーに直接コードを選択できます。 アプリケーションには、ドライバー固有のコードを安全に格納して、これらのドライバーの機能を利用することができます。また、ODBC でサポートされていない機能を使用するためにネイティブデータベース API を呼び出すこともできます。  
  
 ほとんどのカスタムアプリケーションの相互運用性の主な問題は、対象の Dbms が将来変更されるかどうかです。 その場合、このプロセスを簡略化するには、まず、相互運用可能なコードを作成します。 ただし、このような Dbms の変更はめったに発生しません。通常、大量の作業が伴います。 このため、カスタムアプリケーションの開発者は、機能を犠牲にして相互運用性を向上させることはほとんどありません。通常、Dbms を変更するときに、その機能を再度変換することを選択します。
