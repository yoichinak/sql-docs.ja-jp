---
title: SSMA for SAP ASE クライアントのインストール (SybaseToSQL) |Microsoft Docs
description: SAP Adaptive Server Enterprise (ASE) 用の SQL Server Migration Assistant (SSMA) のインストールの前提条件と、のインストール方法について説明します。
ms.custom: ''
ms.date: 07/14/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d9b20774b0a32b0d9d007053bedd2674e79d4e12
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100015372"
---
# <a name="installing-ssma-for-sap-ase-client-sybasetosql"></a>SSMA for SAP ASE クライアントのインストール (SybaseToSQL)

SSMA クライアントは、SAP Adaptive Server Enterprise (ASE) データベースサーバーへの接続、またはまたはのインスタンスへの接続に使用されるプログラムファイルで構成され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ASE データベースオブジェクトをまたは構文に変換し、オブジェクトをまたはに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 読み込み、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] データをまたはに移行し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

このトピックでは、SSMA のインストールの前提条件と手順について説明します。

## <a name="prerequisites"></a>前提条件

SSMA は、SAP ASE 11.9.2 以降のバージョンおよびのすべてのエディションで動作するように設計されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

SSMA をインストールする前に、コンピューターが次の要件を満たしていることを確認してください。

- Windows 7 以降のバージョン、または Windows Server 2008 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー3.1 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)].NET Framework バージョン4.7.2 以降のバージョン。 これは [.NET Framework デベロッパーセンター](https://go.microsoft.com/fwlink/?LinkId=48882)から入手できます。
- Sybase OLE DB/ADO.Net/ODBC プロバイダーと、移行するデータベースが格納されている SAP ASE データベースサーバーへの接続。 プロバイダーは、SAP ASE 製品メディアからインストールできます。 接続の詳細については、「 [SYBASE ASE &#40;SybaseToSQL&#41;への接続 ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)」を参照してください。
- へのアクセス、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] データベースオブジェクトとデータの移行先となる、またはのターゲットインスタンスをホストするコンピューターに対する十分なアクセス許可。 詳細については[ ](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)、「 / [Azure SQL Database &#40;sybasetosql&#41;に接続](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)するための SQL Server &#40;sybasetosql&#41;への接続」を参照してください。
- 4 GB の RAM を推奨します。

## <a name="installing-the-ssma-for-sybase-client"></a>SSMA for Sybase クライアントのインストール

SSMA は Web からダウンロードできます。 最新バージョンをダウンロードするには、 [SQL Server Migration Assistant のダウンロードページ](https://aka.ms/ssmaforsybase)を参照してください。

SSMA クライアントをインストールするには:

1. **SSMAforSybase_ *n*.msi** をダブルクリックします。ここで、 *n* はビルド番号です。
2. [ようこそ] ページで **[次へ]** をクリックします。

   前提条件がインストールされていない場合は、最初に必要なコンポーネントをインストールする必要があることを示すメッセージが表示されます。 すべての前提条件がインストールされていることを確認してから、インストールプログラムを再実行してください。

3. End-User 使用許諾契約書をお読みください。 同意する場合は、 **[同意する] を選択し**、[ **次へ**] をクリックします。
4. [セットアップの種類の選択] ページで、[ **標準**] をクリックします。
5. [ **インストールの準備完了** ] ページで、ツールが開始されるたびにテレメトリと自動更新のチェックを有効または無効にすることができます。 **[インストール]** をクリックしてインストールを開始します。

> [!IMPORTANT]
> 新しいバージョンをインストールする前に、SSMA for Sybase の以前のバージョンをすべてアンインストールしてください。

既定のインストール場所は `C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase` です。

SSMA プログラムファイルに加えて、SSMA for Sybase Extension Pack もインストールする必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [SQL Server &#40;SybaseToSQL&#41;での SSMA コンポーネントのインストール ](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [SQL Server での SSMA コンポーネントのインストール](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
- [Sybase ASE データベースの SQL Server Azure SQL Database への移行](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
