---
description: ODBC コンポーネントのインストール
title: ODBC コンポーネントのインストール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0250cc51b76cbda9c1091ebe1d696c2e569c037f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499748"
---
# <a name="installing-odbc-components"></a>ODBC コンポーネントのインストール
> [!NOTE]  
>  Windows XP および windows Server 2003 以降では、ODBC は Windows オペレーティングシステムに含まれています。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 このセクションでは、ODBC コンポーネントのインストール方法と削除方法について説明します。 ドライバー開発者は常に ODBC コンポーネント (ドライバー) をインストールするため、このセクションを読む必要があります。 アプリケーション開発者は、ODBC コンポーネントをアプリケーションと共に配布する場合にのみ、このセクションを読む必要があります。 ODBC コンポーネントには、ドライバーマネージャー、ドライバー、翻訳者、インストーラー DLL、カーソルライブラリ、および関連ファイルが含まれます。 このセクションでは、odbc アプリケーションは ODBC コンポーネントとは見なされません。  
  
> [!NOTE]  
>  このセクションは、Microsoft Windows プラットフォームに固有のものです。 ODBC コンポーネントを他のプラットフォームにインストールする方法は、プラットフォームによって異なります。  
  
 ODBC コンポーネントは、ファイル単位ではなく、コンポーネントごとにインストールおよび削除されます。 たとえば、変換プログラムがトランスレーター自体と複数のデータファイルで構成されている場合、これらのファイルはグループとしてインストールされ、削除されます。これらのファイルは、ファイルごとにインストールしたり削除したりすることはできません。 その理由は、システムにコンポーネントが完全に存在するようにするためです。  
  
 コンポーネントをインストールおよび削除するために、次のものが ODBC コンポーネントとして定義されています。  
  
-   **コアコンポーネント。** ドライバーマネージャー、カーソルライブラリ、インストーラー DLL、およびその他の関連ファイルによってコアコンポーネントが構成され、グループとしてインストールおよび削除される必要があります。  
  
-   **ドライバ.** 各ドライバーは独立したコンポーネントです。  
  
-   **者.** 各変換プログラムは、独立したコンポーネントです。  
  
 ODBC 3.5 以降で Unicode がサポートされているため、ODBC で OLE DB コンポーネントを使用するには、いくつか考慮する必要があります。 1.1 バージョンの ODBC 用 OLE DB Provider は、ODBC 3.0 内の特定の Unicode 仕様に書き込まれました。 Odbc 3.5 ではこれらの仕様が変更されているため、ODBC 3.5 以降を使用する場合は、バージョン1.5 以降のプロバイダーが必要です。 このセクションでは、次のトピックを扱います。  
  
-   [インストールコンポーネント](../../../odbc/reference/install/installation-components.md)  
  
-   [使用状況のカウント](../../../odbc/reference/install/usage-counting.md)
