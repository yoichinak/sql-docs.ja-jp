---
description: 相互運用可能なアプリケーションの作成
title: 相互運用可能なアプリケーションの作成 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d8bff1848e20705ab64b8284ed42331c80fb23a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421366"
---
# <a name="writing-an-interoperable-application"></a>相互運用可能なアプリケーションの作成
アプリケーションが複数のドライバーに対して同じコードを使用する場合は、そのコードをそれらのドライバー間で相互運用できる必要があります。 ほとんどの場合、これは簡単なタスクです。 たとえば、順方向専用カーソルを使用して行をフェッチするコードは、すべてのドライバーで同じです。 場合によっては、これがより困難になることがあります。 たとえば、SQL ステートメントで使用するための識別子を構築するコードでは、識別子の大文字と小文字の区別、引用符、および3つの部分で構成される名前付け規則を考慮する必要があります。  
  
 一般に、相互運用可能なコードは、機能のサポートおよび機能の可変性の問題に対処する必要があります。 *機能サポート* は、特定の機能がサポートされているかどうかを示します。 たとえば、すべての Dbms でトランザクションをサポートするわけではなく、相互運用可能なコードがトランザクションのサポートに関係なく正しく機能する必要があります。 *特徴の可変性* とは、特定の機能がサポートされている方法の違いを意味します。 たとえば、カタログ名は、一部の Dbms では識別子の先頭に、それ以外の場合は識別子の最後に配置されます。  
  
 アプリケーションでは、デザイン時または実行時に機能のサポートおよび機能の可変性を扱うことができます。 開発者は、デザイン時の機能のサポートと可変性に対処するために、対象の Dbms とドライバーを調べ、同じコードが相互に相互運用できるようにします。 これは一般に、このような問題に対処するために、相互運用性が低いアプリケーションを使用する方法です。  
  
 たとえば、垂直方向のアプリケーションが4つの特定の Dbms でのみ動作することを保証し、各 Dbms でトランザクションがサポートされている場合、アプリケーションは実行時にトランザクションのサポートを確認するコードを必要としません。 トランザクションをサポートするのは、それぞれがトランザクションをサポートする4つの Dbms のみを使用するように設計時に決定されているため、トランザクションは常に使用可能であると想定できます。  
  
 実行時の機能のサポートと変動に対処するには、アプリケーションが実行時にさまざまな機能をテストし、それに応じて動作する必要があります。 これは一般に、相互運用可能なアプリケーションでこれらの問題を処理する方法です。 機能のサポートに関する問題の場合は、機能を省略可能にするコードを記述するか、機能を使用できないときにエミュレートするコードを記述することを意味します。 特徴の可変性の問題の場合、これはすべての可能なバリエーションをサポートするコードを記述することを意味します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [機能のサポートと可変性の確認](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [ウォッチする機能](../../../odbc/reference/develop-app/features-to-watch-for.md)
