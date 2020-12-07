---
description: インストール (ODBC)
title: ソフトウェアのインストール (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], installing
- installing ODBC driver for Oracle [ODBC]
ms.assetid: dfac8ade-eebe-4ebe-a199-feb740ed5bae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe161ef45ef91f67317d7a0b465e00d3d2045c40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449474"
---
# <a name="installing-the-software-odbc"></a>インストール (ODBC)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 ODBC Driver for Oracle は、データアクセスコンポーネントの1つです。 ODBC データソースアドミニストレーターなどの他の ODBC コンポーネントが付属しており、既にインストールされている必要があります。 このドライバーは、Microsoft 製品サポートサービスオンライン Web サイト ( [www.microsoft.com](https://www.microsoft.com)) の「ドライバーとその他のダウンロード」にも記載されています。  
  
 ネットワークソフトウェアは、そのドキュメントに従ってインストールする必要があります。 ODBC Driver for Oracle では、ネットワークソフトウェアがサポートされている限り、特別なインストールの考慮事項は必要ありません。  
  
 Oracle ソフトウェアは、独自のドキュメントに従ってインストールする必要があります。 ODBC Driver for Oracle では、通常、ドライバーがバージョンをサポートしている限り、特別なインストールの考慮事項はありません。 ただし、製品の互換性を維持するには、最新バージョンのドライバーがインストールされていることを確認するために、ODBC Driver for Oracle last をインストールします。 Oracle では、Oracle server 製品およびサーバー製品に付属するクライアントコンポーネントに対する修正プログラムを含む、公開されている FTP サイトを管理します。 これらの修正プログラムは、いくつかの Microsoft 製品およびテクノロジが正しく機能するために必要です。 このサイトの詳細については、「 [Oracle Software 修正プログラム](../../odbc/microsoft/oracle-software-patches.md)」を参照してください。  
  
> [!CAUTION]  
>  MDAC/Windows DAC を介して Oracle ソフトウェアをインストールすると、MDAC の現在のバージョンが上書きされる場合があります。 ODBC コンポーネントを使用して問題が発生した場合は、MDAC を再インストールします。
