---
description: ODBC とは
title: ODBC とは | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 23badedad64ac836f07e3d9f7832fcfa6c33b0b9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428824"
---
# <a name="what-is-odbc"></a>ODBC とは
ODBC に関する多くの誤解がコンピューティング環境に存在します。 エンドユーザーには、Microsoft® Windows®コントロールパネルのアイコンがあります。 アプリケーションプログラマは、データアクセスルーチンを含むライブラリです。 他の多くの場合は、これまでに発生したすべてのデータベースアクセスの問題に対する回答です。  
  
 まず、ODBC はデータベース API の仕様です。 この API は、1つの DBMS またはオペレーティングシステムから独立しています。このマニュアルでは C を使用していますが、ODBC API は言語に依存しません。 ODBC API は、Open Group と ISO/IEC の CLI 仕様に基づいています。 ODBC 3.*x* はこれらの仕様の両方を完全に実装しています。以前のバージョンの ODBC は、これらの仕様の暫定版に基づいていましたが、完全には実装していませんでした。また、スクロール可能なカーソルなど、画面ベースのデータベースアプリケーションの開発者がよく必要とする機能を追加します。  
  
 ODBC API の関数は、DBMS 固有のドライバーの開発者によって実装されています。 アプリケーションは、これらのドライバーの関数を呼び出して、DBMS に依存しない方法でデータにアクセスします。 ドライバーマネージャーは、アプリケーションとドライバー間の通信を管理します。  
  
 Microsoft では、Microsoft Windows®95以降を実行しているコンピューターのドライバーマネージャーを提供していますが、ではいくつかの ODBC ドライバーが記述されており、その一部のアプリケーションから ODBC 関数を呼び出しています。だれでも ODBC アプリケーションやドライバーを書き込むことができます。 実際、現在利用可能な ODBC アプリケーションとドライバーの大部分は、Microsoft 以外の企業によって作成されています。 さらに、ODBC ドライバーとアプリケーションは、Macintosh®およびさまざまな UNIX プラットフォームに存在します。  
  
 Microsoft では、アプリケーションやドライバーの開発者を支援するために、ドライバーマネージャー、インストーラー DLL、テストツール、およびサンプルアプリケーションを提供する Windows 95 以降を実行しているコンピューター用の ODBC ソフトウェア開発キット (SDK) を提供しています。 Microsoft は、これらの Sdk を Macintosh およびさまざまな UNIX プラットフォームに移植するために、Visigenic ソフトウェアと提携しています。  
  
 ODBC はデータベース機能を公開するように設計されているので、補足することは重要です。 そのため、アプリケーションの作成者は、ODBC を使用した単純なデータベースから、完全な機能を備えたリレーショナルデータベースエンジンへの変換が突然行われることを予期していません。 また、ドライバーの作成者は、基になるデータベースに見つからない機能を実装する必要がありません。 ただし、ファイルデータに直接アクセスするドライバー (Xbase ファイルのデータなど) を記述する開発者は、少なくとも最小の SQL 機能をサポートするデータベースエンジンを作成する必要があります。 もう1つの例外として、以前は Microsoft Data Access Components (MDAC) SDK に含まれていた Windows SDK の ODBC コンポーネントには、特定のレベルの機能を実装するドライバーのスクロール可能なカーソルをシミュレートするカーソルライブラリが用意されています。  
  
 ODBC を使用するアプリケーションは、複数のデータベースにまたがる機能を担当します。 たとえば、ODBC は異種結合エンジンではなく、分散トランザクションプロセッサでもありません。 ただし、DBMS に依存しないため、このような複数のデータベースにまたがるツールを構築するために使用できます。
