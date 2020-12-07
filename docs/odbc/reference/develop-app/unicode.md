---
description: Unicode
title: Unicode |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a09a2647175d2b19aa44f1458d0ae8c4ef4565c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424434"
---
# <a name="unicode"></a>Unicode
Unicode では、多くの言語で文字のエンコードを定義します。  
  
 Unicode 標準の詳細については、「 [Unicode コンソーシアム](https://www.unicode.org)」を参照してください。  
  
 Unicode では、ユニバーサル文字セットを定義します。 Windows ANSI コードページでは、通常、1つの言語の文字を含む文字セットを定義します。 異なるコードページを使用するために必要なアプリケーションを作成することは、より困難な場合があります。  
  
 Unicode では、コードページは必要ありません。 すべてのコードポイントは、一部の言語では1つの文字にマップされます。  
  
 現時点では、ODBC でサポートされている唯一の Unicode エンコードは UCS-2 です。これは、16ビット整数 (固定長) を使用して文字を表します。 Unicode では、アプリケーションをさまざまな言語で動作させることができます。  
  
 ODBC 3.5 (またはそれ以降) のドライバーマネージャーでは、Unicode が有効になっています。 これは、関数呼び出しと文字列データ型の2つの主な領域に影響します。 ドライバーマネージャーは、関数の文字列引数と文字列データを、アプリケーションとドライバーの必要に応じてマップします。どちらも、Unicode 対応または ANSI 対応のどちらでもかまいません。 これらの2つの領域については、「 [Unicode 関数の引数](../../../odbc/reference/develop-app/unicode-function-arguments.md) 」と「 [unicode データ](../../../odbc/reference/develop-app/unicode-data.md)」で詳しく説明します。  
  
 ODBC 3.5 (またはそれ以降) のドライバーマネージャーでは、unicode アプリケーションと ANSI アプリケーションの両方を使用した Unicode ドライバーの使用がサポートされています。 Ansi アプリケーションでの ANSI ドライバーの使用もサポートしています。 ドライバーマネージャーでは、ANSI ドライバーを使用する Unicode アプリケーションに対して、Unicode から ANSI へのマッピングが制限されています。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Unicode 関数の引数](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode データ](../../../odbc/reference/develop-app/unicode-data.md)
