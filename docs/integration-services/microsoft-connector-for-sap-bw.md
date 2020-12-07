---
description: Microsoft Connector for SAP BW
title: Microsoft Connector for SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5281f080-53d5-4679-aa26-f4cd4ac7a2df
author: chugugrace
ms.author: chugu
ms.openlocfilehash: af1b8c775991581fadbb25bbf62049194cdc74be
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384891"
---
# <a name="microsoft-connector-for-sap-bw"></a>Microsoft Connector for SAP BW

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW は、SAP NetWeaver BW Version 7 システムからデータを抽出し、このシステムにデータを読み込むための 3 つのコンポーネントのセットで構成されます。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW for SQL Server 2016 は、SQL Server 2016 の Feature Pack のコンポーネントです。 Connector for SAP BW およびそのドキュメントをインストールするには、 [SQL Server 2016 Feature Pack Web ページ](https://www.microsoft.com/download/details.aspx?id=56833)からインストーラーをダウンロードして実行します。  

> [!IMPORTANT]
> Microsoft では、更新されたバージョンの Connector for SAP BW を提供する予定はありません。 サード パーティによって開発されているため、Microsoft は SAP BW コンポーネントのソース コードを所有していません。そのため、ソース コードの更新はできません。 [Theobald Software](https://theobald-software.com/en/xtract-is-productinfo.html) などの Microsoft ISV パートナーからの最新の SAP 接続コンポーネントの購入を検討してください。 Microsoft の ISV パートナーは、Azure で SSIS をインストールするために SAP 接続コンポーネントを適応させています。
 
> [!IMPORTANT]  
>  Microsoft Connector for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
## <a name="components"></a>コンポーネント  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW には次のコンポーネントがあります。  
  
-   **SAP BW 変換元** - SAP BW 変換元は、SAP Netweaver BW Version 7 システムからデータを抽出するためのデータ フローの変換元コンポーネントです。  
  
-   **SAP BW 変換先** - SAP BW 変換先は、SAP Netweaver BW Version 7 システムにデータを読み込むためのデータ フローの変換先コンポーネントです。  
  
-   **SAP BW 接続マネージャー** - SAP BW 接続マネージャーによって、SAP Netweaver BW Version 7 システムに SAP BW 変換元または SAP BW 変換先が接続されます。  
  
 SAP BW 接続マネージャー、変換元、変換先の構成および使用方法の詳細については、ホワイト ペーパー「 [SAP BI 7.0 を使用した SQL Server Integration Services](/previous-versions/sql/sql-server-2008/dd299430(v=sql.100))」を参照してください。 このホワイト ペーパーには、SAP BW で必要なオブジェクトの構成方法についても説明されています。  
  
## <a name="documentation"></a>ドキュメント  
 この [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW のヘルプ ファイルには、次のトピックとセクションが含まれています。  
  
 [Microsoft Connector for SAP BW のインストール](../integration-services/installing-the-microsoft-connector-for-sap-bw.md)  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW のインストール要件について説明します。  
  
 [Microsoft Connector for SAP BW のコンポーネント](../integration-services/microsoft-connector-for-sap-bw-components.md)  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW の各コンポーネントについて説明します。  
  
 [Microsoft Connector for SAP BW の F1 ヘルプ](../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW の各コンポーネントのユーザー インターフェイスについて説明します。  
  
