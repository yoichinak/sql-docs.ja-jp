---
description: SMO のインストール
title: SMO | をインストールするMicrosoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15ce6ea1c72bee64ad8fe96e70b9a7c513c623e6
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868275"
---
# <a name="installing-smo"></a>SMO のインストール

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

このページでは、アプリケーションで使用する SMO をインストールする方法と、SMO を使用するためのシステム要件について説明します。

## <a name="smo-nuget-package"></a>SMO NuGet パッケージ

2017以降 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、smo は [SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet パッケージとして配布され、ユーザーは smo を使用してアプリケーションを開発できるようになります。

これは SharedManagementObjects.msi に代わるものであり、SQL Server の各リリースの SQL Feature Pack の一部としてリリースされています。 SMO を使用するアプリケーションは、代わりに NuGet パッケージを使用するように更新する必要があり、開発中のアプリケーションと共にバイナリが確実にインストールされるようにします。

>>[!Important]
>>「 [ファイルとバージョン番号](files-and-version-numbers.md) 」ページで説明したように、SMO アセンブリを GAC にインストールすることはできません。 これを行うと、他のアプリケーションで問題が発生する可能性があります。これらのアプリケーションは、これらのバージョンの SMO (Management Studio など) も使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。

## <a name="installing-the-package"></a>パッケージのインストール

Nuget パッケージのインストールと使用の手順と例については、「 [nuget クイックスタート-パッケージを使用](/nuget/quickstart/use-a-package) する」を参照してください。 
  
## <a name="system-requirements"></a>システム要件
  
 SMO [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] では、4.0 または .Net Core 2.0 が実行されている必要があるため、これを使用するアプリケーションでは、クライアントコンピューターがそのバージョン以降をインストールしていることを確認する必要があります。 NetFx SMO ライブラリと共にインストールされる一部のネイティブバイナリでは、VC 2013 ランタイムもインストールする必要があります。このランタイムはパッケージに含まれていません。 ターゲットアーキテクチャに適した再頒布可能ファイルは、 https://www.microsoft.com/download/details.aspx?id=40784
