---
description: セットアップ プログラム
title: セットアッププログラム |Microsoft Docs
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4cd4858214ff084a037002abd3bd34035160496b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421326"
---
# <a name="setup-program"></a>セットアップ プログラム
> **注:** Windows XP および windows Server 2003 以降で **は、ODBC は windows オペレーティングシステムに含まれて**います。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 ユーザーはセットアッププログラムを実行してセットアッププロセスを開始します。 セットアッププログラムは、アプリケーションまたはドライバーの開発者によって作成されます。 ODBC コンポーネントをインストールするだけでなく、他のソフトウェアをインストールすることもできます。 たとえば、アプリケーション開発者は、同じセットアッププログラムを使用して ODBC コンポーネントをインストールし、アプリケーションをインストールすることができます。  
  
 開発者は、Microsoft® Windows® SDK セットアップユーティリティを使用して、または他のベンダーからセットアップソフトウェアを使用して、セットアッププログラムを最初から作成できます。 これにより、開発者はセットアッププログラムのルックアンドフィールを完全に制御できます。 セットアッププログラムを記述して、ODBC アプリケーションなどの追加ソフトウェアをインストールすることができます。 Windows SDK セットアップユーティリティの詳細については、Windows SDK のドキュメントを参照してください。  
  
 セットアッププログラムによって実際に実行されるインストールの量は、インストーラー DLL で呼び出す機能によって異なります。 インストーラー DLL には、個々の ODBC コンポーネントをインストールするための関数が含まれています。 セットアッププログラムでは、単純に、インストーラー DLL 内の **Sqlinstalldrivermanager**、 **sqlinstalldrivermanager**、または **SQLInstallTranslatorEx** を呼び出して、コンポーネントをインストールするディレクトリのパスを取得し、コンポーネントに関する情報をレジストリに追加します。 これらの関数は、実際にはファイルをコピーしません。セットアッププログラムは、これらの関数の引数の情報を使用してこれを行います。  
  
 インストーラー DLL には、ODBC コンポーネントを削除する関数も含まれています。 セットアッププログラムは、インストーラー DLL 内の **Sqlremovedrivermanager**、 **sqlremovedriver**、または **sqlremovetranslator** を呼び出して、レジストリ内のコンポーネントの使用状況カウントをデクリメントします。また、コンポーネントの新しい使用率が0になった場合は、コンポーネントに関するすべての情報をレジストリから削除します。 これらの関数は、実際にはコンポーネントのファイルを削除しません。新しい使用状況カウントが0になると、セットアッププログラムはこれを行います。
