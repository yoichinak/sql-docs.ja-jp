---
description: 32 ビット ドライバーで 16 ビット アプリケーションを使用
title: 32ビットドライバーで16ビットアプリケーションを使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c54dc53e5a8e6d3322bfa74ec6904cebca434b8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471389"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>32 ビット ドライバーで 16 ビット アプリケーションを使用
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 代わりに、32ビットまたは64ビットのドライバーマネージャーを使用してください。  
  
 32ビットドライバーがスレッドを作成する Win32 API 関数を明示的に呼び出すのでない限り、Windows ベースのシステムでは、32ビットのドライバーを使用して16ビットアプリケーションを実行できます。 Windows on Windows (WOW) サブシステムは、16ビットモードでアプリケーションを実行し、オペレーティングシステムの16ビット呼び出しを解決します。 ODBC のサンク Dll は、アプリケーションから32ビットのドライバーへの16ビットの呼び出しを解決します。 16ビットアプリケーションは Windows API を使用し、32ビットドライバーは Win32 API を使用します。  
  
## <a name="architecture"></a>Architecture  
 次の図は、16ビットアプリケーションが32ビットドライバーと通信する方法を示しています。 16ビットドライバーマネージャーと32ビットドライバーは、16ビット ODBC 呼び出しを32ビット ODBC 呼び出しに変換する汎用のサンク Dll です。  
  
 ![16&#45;ビットアプリが 32&#45;ビットドライバーと通信する方法](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  16ビットアプリケーションが32ビットドライバーと対話する場合、32ビットドライバーマネージャーは常に、ドライバーでサポートされている ODBC のバージョンとして "2.0" を返します。  
  
## <a name="administration"></a>管理  
 32ビットドライバーのデータソースは、ODBC データソースアドミニストレーターを使用して管理できます。 Microsoft® Windows®2000を実行しているコンピューターで ODBC アドミニストレーターを開くには、Windows のコントロールパネルを開き、[ **管理ツール**] をダブルクリックし、[ **データソース (ODBC)**] をダブルクリックします。 以前のバージョンの Microsoft Windows を実行しているコンピューターでは、このアイコンは、 **32 ビット odbc** または単に **odbc**という名前になっています。  
  
 次の図は、16ビットアプリケーションが32ビットドライバーのセットアップ DLL を呼び出す方法を示しています。 16ビットインストーラー dll と32ビットドライバーセットアップ DLL は、16ビットインストーラー DLL 呼び出しを32ビットインストーラー DLL 呼び出しに変換する汎用のサンク DLL です。  
  
 ![16&#45;ビットアプリが 32&#45;ビットドライバーのセットアップ DLL を呼び出す方法](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 Windows 上の Windows (16 ビットから32ビットのサンキング) では、Ds32gt.dll という名前の追加のサンキング DLL が、32ビットのセットアップ DLL を通じて渡された16ビットの引数値を16ビットに変換します。  
  
## <a name="components"></a>コンポーネント  
 MDAC 2.8 SP1 SDK の ODBC コンポーネントには、32ビットドライバーで16ビットアプリケーションを実行するための次のファイルが含まれています。 これらのコンポーネントは、\ Redist ディレクトリにあります。  
  
|ファイル名|説明|  
|---------------|-----------------|  
|Odbc16gt.dll|16ビット ODBC 汎用サンク DLL|  
|Odbc32gt.dll|32ビット ODBC 汎用サンク DLL|  
|Odbccp32.dll|32-ビットインストーラー DLL|  
|Odbcad32.exe|32ビット管理者プログラム|  
|Odbcinst .hlp|インストーラーヘルプファイル|  
|Ds16gt.dll|16ビットドライバーセットアップ汎用サンク DLL|  
|Ctl3d32.dll|32ビット3次元ウィンドウスタイルライブラリ|  
  
 また、ODBC 3.51 に含まれていない16ビット ODBC 2.10 ドライバーマネージャーと共に次のファイルが必要です。これは、16ビットアプリケーションと共にインストールする必要があります。  
  
|ファイル名|説明|  
|---------------|-----------------|  
|Odbc.dll|16ビットドライバーマネージャー|  
|Odbcinst.dll|16ビットインストーラー DLL|  
|Odbcadm.exe|16ビット ODBC 管理者プログラム|
