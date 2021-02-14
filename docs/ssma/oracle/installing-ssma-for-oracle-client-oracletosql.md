---
title: SSMA for Oracle クライアントのインストール (OracleToSQL) |Microsoft Docs
description: Oracle クライアント用の SQL Server Migration Assistant (SSMA) のインストールの前提条件と、のインストール方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5bed1589c0852acc2d782028f6b9cc253301babe
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100073494"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>SSMA for Oracle クライアントのインストール (OracleToSQL)

SSMA クライアントは、次のタスクを実行するプログラムファイルで構成されています。  
  
- Oracle データベースに接続します。
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する。
- Oracle データベースオブジェクトを構文に変換 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。
- オブジェクトをに読み込み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。
- データをに移行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。

このトピックでは、SSMA のインストールの前提条件と手順について説明します。

## <a name="prerequisites"></a>前提条件

SSMA は、Oracle 9 以降のバージョンおよびのすべてのエディションで動作するように設計されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

SSMA をインストールする前に、コンピューターが次の要件を満たしていることを確認してください。

- Windows 7 以降のバージョン、または Windows Server 2008 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー3.1 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] バージョン4.7.2 以降のバージョン。 これは [.NET Framework デベロッパーセンター](https://go.microsoft.com/fwlink/?LinkId=48882)から入手できます。
- 移行する Oracle データベースへの接続。
- へのアクセス、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] データベースオブジェクトとデータの移行先となる、またはのターゲットインスタンスをホストするコンピューターに対する十分なアクセス許可。 詳細については、「 [SQL Server &#40;OracleToSQL&#41;への接続 ](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)」を参照してください。
- 4 GB の RAM を推奨します。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>SSMA for Oracle クライアントのインストール

SSMA は Web からダウンロードできます。 最新バージョンをダウンロードするには、 [SQL Server Migration Assistant のダウンロードページ](https://aka.ms/ssmafororacle)を参照してください。

SSMA クライアントをインストールするには:

1. **SSMAforOracle_ *n*.msi** をダブルクリックします。ここで、 *n* はビルド番号です。
2. [ようこそ] ページで **[次へ]** をクリックします。

   前提条件がインストールされていない場合は、最初に必要なコンポーネントをインストールする必要があることを示すメッセージが表示されます。 すべての前提条件がインストールされていることを確認してから、インストールプログラムを再実行してください。  

3. End-User 使用許諾契約書をお読みください。 同意する場合は、 **[同意する] を選択し**、[ **次へ**] をクリックします。
4. [ **セットアップの種類の選択** ] ページで、[ **標準**] をクリックします。
5. [ **インストールの準備完了** ] ページで、ツールが開始されるたびにテレメトリと自動更新のチェックを有効または無効にすることができます。 **[インストール]** をクリックしてインストールを開始します。

> [!IMPORTANT]
> 新しいバージョンをインストールする前に、SSMA for Oracle の以前のバージョンをすべてアンインストールしてください。

既定のインストール場所は `C:\Program Files\Microsoft SQL Server Migration Assistant for Oracle` です。

SSMA プログラムファイルに加えて、SSMA for Oracle Extension Pack もインストールする必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [SQL Server での SSMA コンポーネントのインストール](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [SQL Server での SSMA コンポーネントのインストール](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)
- [SQL Server への Oracle データベースの移行](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
