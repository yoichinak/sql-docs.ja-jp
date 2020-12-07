---
description: 32 ビット ドライバーで 32 ビット アプリケーションを使用
title: 32ビットドライバーで32ビットアプリケーションを使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69005071c83047471e76f38160265bc35cdccd4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471366"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>32 ビット ドライバーで 32 ビット アプリケーションを使用
32ビットのドライバーを使用して、32ビットのアプリケーションを実行できます。 32ビットアプリケーションと32ビットドライバーは、Win32® API を使用します。  
  
## <a name="architecture"></a>Architecture  
 次の図は、32ビットアプリケーションが32ビットドライバーと通信する方法を示しています。 アプリケーションは、32ビットドライバーマネージャーを呼び出し、それによって32ビットドライバーが呼び出されます。  
  
 ![32&#45;ビットアプリが 32&#45;ビットドライバーと通信する方法](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  WindowsNT/Windows2000 では、32ビットのサンキングインストーラー DLL を使用しないでください。 32ビットインストーラー DLL と同じファイル名が付いていますが、DLL は異なります。  
  
## <a name="administration"></a>管理  
 32ビットドライバーのデータソースは、ODBC データソースアドミニストレーターを使用して管理できます。 Windows 2000 を実行しているコンピューターで ODBC アドミニストレーターを開くには、Windows のコントロールパネルを開き、[ **管理ツール**] をダブルクリックしてから、[ **データソース (ODBC)**] をダブルクリックします。 以前のバージョンの Microsoft Windows を実行しているコンピューターでは、このアイコンは、 **32 ビット odbc** または単に **odbc**という名前になっています。  
  
## <a name="components"></a>コンポーネント  
 ODBC コンポーネントには、32ビットのドライバーを使用して32ビットアプリケーションを実行するための次のファイルが含まれています。 これらのコンポーネントは、\ Redist ディレクトリにあります。  
  
|ファイル名|説明|  
|---------------|-----------------|  
|Odbc32.dll|32-ビットドライバーマネージャー|  
|Odbccp32.dll|32-ビットインストーラー DLL|  
|Odbcad32.exe|32ビット ODBC 管理者プログラム|  
|Odbcinst .hlp|インストーラーヘルプファイル|  
|Msvcrt40.dll|C ランタイムライブラリ|
