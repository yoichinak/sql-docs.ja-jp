---
title: SSMA for DB2 クライアントのインストール (DB2ToSQL) |Microsoft Docs
description: DB2 クライアント用の SQL Server Migration Assistant (SSMA) とのインストールの前提条件について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a223f5dbf6e100ac776e2f3aebad51c9bb885abf
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869610"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>SSMA for DB2 クライアントのインストール (DB2ToSQL)

SSMA クライアントは、次のタスクを実行するプログラムファイルで構成されています。

- DB2 データベースに接続します。
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する。
- DB2 データベースオブジェクトを構文に変換 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。
- オブジェクトをに読み込み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。
- データをに移行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。

このトピックでは、SSMA のインストールの前提条件と手順について説明します。

## <a name="prerequisites"></a>前提条件

SSMA は、z/OS バージョン9.0 および10.0、DB2 on LUW バージョン9.8 および10.1 以降のバージョン、db2 for i バージョン7.1 以降、またはそれ以降のバージョンの db2 と連携して動作するように設計されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

SSMA をインストールする前に、コンピューターが次の要件を満たしていることを確認してください。

- Windows 7 以降のバージョン、または Windows Server 2008 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー3.1 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] バージョン4.7.2 以降のバージョン。 これは [.NET Framework デベロッパーセンター](https://go.microsoft.com/fwlink/?LinkId=48882)から入手できます。
- Microsoft OLE DB Provider for DB2 バージョン5以降のバージョン、および移行する DB2 データベースへの接続。
- にアクセスし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースオブジェクトとデータを移行する、または Azure SQL Database のターゲットインスタンスをホストするコンピューターに対して十分なアクセス許可を付与します。 詳細については、「 [SQL Server &#40;DB2ToSQL&#41;への接続 ](../../ssma/db2/connecting-to-sql-server-db2tosql.md)」を参照してください。
- 4 GB の RAM を推奨します。

## <a name="microsoft-ole-db-provider-for-db2"></a>Microsoft OLE DB Provider for DB2

OLE DB provider for DB2 バージョン6.0 をダウンロードするには、 [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992)」を参照してください。

SSMA は Web からダウンロードできます。 最新バージョンをダウンロードするには、 [SQL Server Migration Assistant のダウンロードページ](https://aka.ms/ssmafordb2)を参照してください。

SSMA クライアントをインストールするには:

1. **SSMAforDB2_ *n*.msi** をダブルクリックします。ここで、 *n* はビルド番号です。
2. **[ようこそ]** ページで **[次へ]** をクリックします。

   前提条件がインストールされていない場合は、最初に必要なコンポーネントをインストールする必要があることを示すメッセージが表示されます。 すべての前提条件がインストールされていることを確認してから、インストールプログラムを再実行してください。

3. End-User 使用許諾契約書をお読みください。 同意する場合は、 **[同意する] を選択し**、[ **次へ**] を選択します。
4. [ **セットアップの種類の選択** ] ページで、[ **標準**] を選択します。
5. [ **インストールの準備完了** ] ページで、ツールが開始されるたびにテレメトリと自動更新のチェックを有効または無効にすることができます。 **[インストール]** をクリックしてインストールを開始します。

> [!IMPORTANT]
> 新しいバージョンをインストールする前に、SSMA for DB2 の以前のバージョンをすべてアンインストールしてください。

既定のインストール場所は `C:\Program Files\Microsoft SQL Server Migration Assistant for DB2` です。

## <a name="see-also"></a>関連項目

- [SQL Server での SSMA コンポーネントのインストール](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)
- [DB2 データベースの SQL Server への移行](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)
