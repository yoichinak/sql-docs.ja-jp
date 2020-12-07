---
description: ODBC Driver for Oracle
title: ODBC Driver for Oracle |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a561539ff960dfa6691d26496b1b62d2ee8ae763
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449334"
---
# <a name="odbc-driver-for-oracle"></a>ODBC Driver for Oracle
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 Microsoft® ODBC Driver for Oracle を使用すると、ODBC 準拠のアプリケーションを Oracle データベースに接続できます。 ODBC Driver for Oracle は、 *Odbc プログラマーズリファレンス*で説明されている OPEN DATABASE CONNECTIVITY (odbc) 仕様に準拠しています。 これにより、インターネットインフォメーションサービス (IIS) 内からの PL/SQL パッケージ、XA/DTC 統合、および Oracle アクセスにアクセスできるようになります。  
  
 Oracle RDBMS は、さまざまなワークステーションおよび minicomputer オペレーティングシステムで実行されるマルチユーザーリレーショナルデータベース管理システムです。 Microsoft Windows を実行している IBM と互換性のあるコンピューターは、ネットワーク経由で Oracle データベースサーバーと通信できます。 サポートされているネットワークには、Microsoft LAN Manager、NetWare、VINES、DECnet、TCP/IP をサポートする任意のネットワークなどがあります。  
  
 ODBC Driver for Oracle を使用すると、アプリケーションは ODBC インターフェイスを介して Oracle データベースのデータにアクセスできます。 ドライバーは、ローカルの Oracle データベースにアクセスできます。また、SQL * Net を介してネットワークと通信することもできます。 次の図は、このアプリケーションとドライバーのアーキテクチャの詳細を示しています。  
  
 ![ODBC Driver for Oracle app&#47;ドライバーのアーキテクチャ](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 ODBC Driver for Oracle は、API の準拠レベル1と SQL 適合性レベルのコアに準拠しています。 また、API 準拠レベル2の一部の関数、およびコアと拡張 SQL の準拠レベルの文法のほとんどもサポートしています。 ドライバーは ODBC 2.5 に準拠し、32ビットシステムをサポートしています。 Oracle 7.3 x は完全にサポートされています。Oracle8 のサポートは限られています。 ODBC Driver for Oracle では、新しい Oracle8 データ型 (Unicode データ型、Blob、CLOBs) はサポートされていません。また、Oracle の新しいリレーショナルオブジェクトモデルもサポートしていません。 サポートされているデータ型の詳細については、このガイドの「 [サポートされるデータ型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) 」を参照してください。  
  
 Oracle データにアクセスするには、次のコンポーネントが必要です。  
  
-   ODBC Driver for Oracle  
  
-   Oracle RDBMS データベース  
  
-   Oracle クライアントソフトウェア  
  
 また、リモート接続の場合は次のようになります。  
  
-   ドライバーとデータベースを実行しているコンピューターを接続するネットワーク。 ネットワークは、SQL * Net 接続をサポートしている必要があります。  
  
## <a name="component-documentation"></a>コンポーネントのドキュメント  
 このガイドでは、Microsoft ODBC Driver for Oracle の設定と構成、およびプログラムによる機能の追加について詳しく説明します。 また、テクニカルリファレンス資料も含まれています。  
  
 特定の Oracle 製品の動作に関する詳細については、Oracle 製品に付属のドキュメントを参照してください。  
  
 ODBC データソースアドミニストレーターを使用した Microsoft ODBC Driver for Oracle の設定または構成の詳細については、 [Odbc データソースアドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md) のドキュメントを参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ODBC Driver for Oracle ユーザー ガイド](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [ODBC Driver for Oracle プログラマー向けリファレンス](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
