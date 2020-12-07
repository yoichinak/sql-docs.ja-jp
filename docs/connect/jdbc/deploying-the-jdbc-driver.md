---
title: JDBC ドライバーの展開
description: 使用するアプリケーションと共に Microsoft JDBC Driver for SQL Server を再配布して展開する方法と、必要なファイルについて説明します。
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 08365944acd071f21b3b4fadf950c23b65c6cfe5
ms.sourcegitcommit: b80364e31739d7b08cc388c1f83bb01de5dd45c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87565432"
---
# <a name="deploying-the-jdbc-driver"></a>JDBC ドライバーの展開

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] に依存するアプリケーションを展開する場合、使用するアプリケーションと共に JDBC ドライバーを再配布する必要があります。 Windows オペレーティング システムのコンポーネントである Windows Data Access Component (Windows DAC) とは異なり、JDBC ドライバーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンポーネントであると見なされます。  
  
アプリケーションと共に JDBC ドライバーを展開する方法には 2 種類あります。 1 つは、JDBC ドライバーのファイルを、独自のカスタム インストール パッケージの一部として含める方法です。 2 つ目の方法では、Microsoft によって提供される JDBC インストール パッケージを使用します。これは、[Microsoft JDBC Driver for SQL Server のダウンロード ページ](download-microsoft-jdbc-driver-for-sql-server.md)からダウンロードできます。  
  
以下のセクションでは、Windows および UNIX オペレーティング システム上で JDBC インストール パッケージを使用する方法について説明します。  
  
> [!NOTE]  
> 一般的な Java アプリケーションの展開については、Java の Web サイトを参照してください。  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Windows システム上での JDBC ドライバーの展開

Windows オペレーティング システム上で JDBC ドライバーを展開する場合、zip 形式のインストール パッケージをアンパックする必要があります。これは通常、`sqljdbc_<version>_<language>.zip` という名前です。

## <a name="deploying-the-driver-on-unix-systems"></a>UNIX システム上での JDBC ドライバーの展開

UNIX オペレーティング システム上で JDBC ドライバーを展開する場合、GZIP ファイル形式のインストール パッケージを使用する必要があります。これは通常、`sqljdbc_<version>_<language>.tar.gz` という名前です。  
  
JDBC ドライバーをインストールする前に、gzip ユーティリティおよび tar ユーティリティの両方がユーザーのシステム上にインストールされ、これらのユーティリティの実行可能ファイルを含むフォルダーが PATH 環境変数に追加されていることを確認します。  
  
zip 形式の tar ファイルをアンパックするには、ドライバーをアンパックするディレクトリに移動し、次のコマンドを入力します。  
  
`gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
tar ファイルをアンパックするには、ドライバーをインストールするディレクトリに tar ファイルを移動し、次のコマンドを入力します。  
  
`tar -xf sqljdbc_<version>_<language>.tar`  

## <a name="legalities-of-driver-redistribution"></a>ドライバーの再配布の合法性

JDBC Driver ドライバー 6.0、6.2、6.4、7.0、7.2、7.4、8.2、8.4 は再配布可能です。 ライセンス契約の "_再頒布可能コード_" の条項をご確認ください。

JDBC Driver バージョン 4.x は、旧バージョンです。 4\.x のサポートは 2018 までに有効期限が切れています。

## <a name="see-also"></a>関連項目

[JDBC ドライバーの概要](overview-of-the-jdbc-driver.md)  
