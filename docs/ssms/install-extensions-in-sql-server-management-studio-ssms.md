---
description: SQL Server Management Studio (SSMS) への拡張機能のインストール
title: SQL Server Management Studio (SSMS) への拡張機能のインストール
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
keywords:
- 拡張機能
- vsix
- 拡張機能のインストール
- vsix のインストール
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 07/29/2020
ms.openlocfilehash: bf4c9ee5287a2e0fdecf8455334561ce130499bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492047"
---
# <a name="install-extensions-in-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) への拡張機能のインストール

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

SQL Server Management Studio (SSMS) 拡張機能は、Visual Studio の "Visual Studio 拡張機能の開発" ワークロードを使用して、C# で作成されます。 SSMS 18.x は、Visual Studio 2017 Shell 上に構築され、その環境の制限の対象となります。

SSMS 18.x への拡張機能をインストールするには、Visual Studio または独立したマネージド パッケージ インストーラーを使用して、VSIX を展開します。  Visual Studio での展開については、以下で説明します。

> [!NOTE]
> SQL Server Management Studio 拡張機能は、SSMS 18.x の VSIXInstaller でインストールすることはできません。
  
## <a name="visual-studio-deployment-of-an-extension-for-ssms-18x"></a>SSMS 18.x 向けの拡張機能の Visual Studio での展開

拡張機能を手動でインストールするには、関連付けられている拡張ファイル (VSIX) を既定の SSMS 拡張機能フォルダーにコピーします。  SSMS では、起動時にこのフォルダーの拡張子が自動的に確認されます。  VSIX の展開は、プロジェクトのビルド時に、Visual Studio によって実行されます。 

  
1.  SSMS のインストールと既定の拡張機能フォルダーを検索します。  SSMS の既定のインストール設定でのフォルダーの場所は ```C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\Extensions\``` です。  


2. Visual Studio を管理者として起動します。

3.  ビルド時に Visual Studio でファイルのコピー プロセスを完了させるには、プロジェクトの [プロパティ] ウィンドウの [VSIX] タブにある [Copy VSIX content to the following location]\(VSIX のコンテンツを次の場所にコピーする\) チェックボックスをオンにします。 チェックボックスの下にあるテキストボックスに、この拡張機能のフォルダーが追加されている上記のフォルダーの場所を入力します。  例: ```C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\Extensions\SampleExtension```
  
![チェックボックスが 3 つ、テキスト ボックスが 1 つあるプロジェクトのプロパティ ウィンドウの VSIX 設定](./media/install-extensions/vsix_ssms.png)

4. 拡張機能プロジェクトをビルドします。ビルドが正常に完了すると、拡張ファイルが SSMS 拡張機能フォルダーに転送されます。

5.  SSMS を起動して、拡張機能をテストします。
  
