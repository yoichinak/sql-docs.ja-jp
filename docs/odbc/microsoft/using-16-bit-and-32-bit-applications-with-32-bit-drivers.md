---
description: 32 ビット ドライバーで 16 ビットおよび 32 ビット アプリケーションを使用
title: 32ビットドライバーで16ビットおよび32ビットのアプリケーションを使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3985fa6fa4fd24ad9638e418915542b48abc26f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471377"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>32 ビット ドライバーで 16 ビットおよび 32 ビット アプリケーションを使用
> [!IMPORTANT]  
>  16ビットアプリケーションのサポートは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、32ビットまたは64ビットのアプリケーションを開発します。  
  
 ODBC データアクセスコンポーネントでは、32ビットドライバーで16ビットアプリケーションと32ビットアプリケーションを使用できます。 Microsoft® Windows®95/98 および Microsoft Windows NT®/windows 2000 オペレーティングシステムでは、次のアプリケーションとドライバーの組み合わせがサポートされています。  
  
-   32ビットドライバーを使用する16ビットアプリケーション  
  
-   32ビットドライバーを使用する32ビットアプリケーション  
  
 16ビットドライバーでの32ビットアプリケーションの使用はサポートされていません。  
  
> [!NOTE]  
>  ODBC バージョン3.0 のリリース以降、Windows NT 4.0 がサポートされるようになりました。  
  
 ODBC には、上記の構成をサポートするために必要な ODBC コンポーネントが含まれています。これは、"サンク" ダイナミックリンクライブラリ (Dll) によって、16ビットアドレスから32ビットアドレスへの変換、およびその逆の変換を行います。 セットアッププログラムによって、使用しているオペレーティングシステムが特定され、そのシステムに必要な ODBC コンポーネントがインストールされます。 また、すべてのシステムで使用される ODBC コンポーネントをインストールするように選択することもできます。  
  
 ほとんどの場合、アプリケーションまたはドライバーを16ビットから32ビットに移植するには、次の5種類の変更が必要です。  
  
-   メッセージ処理コードの変更  
  
-   整数とハンドルが32ビットであるための変更  
  
-   Windows アプリケーションプログラミングインターフェイス (Api) の呼び出しの変更  
  
-   ドライバーをスレッドセーフにするための変更  
  
-   ODBC コンポーネントの変更点  
  
 アプリケーションまたはドライバーのプログラミングの観点からは、16ビットと32ビットの ODBC コンポーネントの主な違いは、ファイル名が異なることです。 システムの観点から見ると、各アプリケーションまたはドライバー接続のアーキテクチャは異なり、データソースの管理に使用されるツールは異なります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [32 ビット ドライバーで 16 ビット アプリケーションを使用](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [32 ビット ドライバーで 32 ビット アプリケーションを使用](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
