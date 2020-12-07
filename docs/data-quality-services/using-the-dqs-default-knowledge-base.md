---
description: DQS の既定のナレッジ ベースの使用
title: DQS の既定のナレッジ ベースの使用
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: swinarko
ms.author: sawinark
ms.openlocfilehash: a6967254559dda05fcedd1224a8b8769b08f10ed
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724658"
---
# <a name="using-the-dqs-default-knowledge-base"></a>DQS の既定のナレッジ ベースの使用

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 **(DQS) にインストールされている既定のナレッジ ベース、** DQS データ [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] について説明します。 これは、次のドメインを含む、あらかじめ構築された既定のナレッジ ベースです。  
  
-   **国/地域**: 各地域の通常の長い名前 (国/地域が指定した公式名) と短縮名 (一覧やマップなどで一般に使用される名前)、2 文字の省略形、3 文字の省略形、各地域の 3 桁のコードが含まれます。  先頭の値は長い名前に設定されます。  
  
-   **国/地域 (3 文字が先頭)**: 各地域の通常の長い名前 (国/地域が指定した公式名) と短縮名 (一覧やマップなどで一般に使用される名前)、2 文字の省略形、3 文字の省略形、および 3 桁のコードが含まれます。  先頭の値は、3 文字の省略形に設定されます。  
  
-   **国/地域 (2 文字が先頭)**: 各地域の通常の長い名前 (国/地域が指定した公式名) と短縮名 (一覧やマップなどで一般に使用される名前)、2 文字の省略形、3 文字の省略形、各地域の 3 桁のコードが含まれます。  先頭の値は、2 文字の省略形に設定されます。  
  
-   **米国 - 郡**: 米国の郡の一覧が含まれています。  
  
-   **米国 - 姓**: 2000 年の国勢調査で 100 例以上登録された姓の一覧です。  
  
-   **米国 - 場所 -**: 2010 年の国勢調査から抽出された、50 州、コロンビア特別区、およびプエルトリコの地域の一覧です。  
  
-   **米国 - 州**: 米国の各州の通常の長い (公式) の名前と 2 文字の省略形が含まれます。 先頭の値は通常の州名に設定されます。  
  
-   **米国 - 州 (2 文字の省略形)**: 米国の各州の通常の長い (公式) の名前と 2 文字の省略形が含まれます。 先頭の値は、州名の 2 文字の省略形に設定されます。  
  
## <a name="using-the-default-knowledge-base"></a>既定のナレッジ ベースの使用  
 既定の DQS ナレッジ ベースである DQS データは、次の方法で使用します。  
  
-   既定のナレッジ ベースを使用してクレンジング データ品質プロジェクトを開始して実行します。先に DQS の新しいナレッジ ベースを作成する必要はありません。  
  
-   既定のナレッジ ベースで、ドメイン管理、ナレッジ検出、または照合ポリシーのアクティビティを実行します。 これを実行するには、 **Data Quality Client Home Screen** の [[ナレッジ ベースを開く]](../data-quality-services/data-quality-client-home-screen.md)をクリックし、 **[ナレッジ ベースを開く]** 画面の **[DQS Data]** ナレッジ ベースを選択して、 **[アクティビティの選択]** 領域で必要なアクティビティを選択します。 **[次へ]** をクリックして続行します。  
  
-   既定のナレッジ ベースを使用して新しいナレッジ ベースを作成します。 既存のナレッジ ベースからナレッジ ベースを作成する方法については、「 [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md)」を参照してください。  
  
-   「 [Integration Services の DQS クレンジング コンポーネント](/previous-versions/sql/sql-server-2012/ee677619(v=sql.110)) 」および「 [Excel 用マスター データ サービス アドイン](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)」で、それを使用します。  
  
## <a name="see-also"></a>参照  
 [DQS のナレッジ ベースとドメイン](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
