---
title: データ処理拡張機能の概要 | Microsoft Docs
description: Reporting Services に付属するデータ処理拡張機能を紹介し、カスタムのデータ処理をレポート サーバーに追加する方法について説明します。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], about extensions
ms.assetid: 1d652605-9313-4c75-98b4-ba4dcbbb222d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 61c30aa9214b87e9acf74dc12d71dd9e8e6d6fa5
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100061187"
---
# <a name="data-processing-extensions-overview"></a>データ処理拡張機能の概要
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータ処理拡張機能を使用することによって、データ ソースに接続し、データを取得できます。 データ処理拡張機能は、データ ソースとデータセット間のブリッジとしても機能します。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータ処理拡張機能は、[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] データ プロバイダー インターフェイスのサブセットに倣っています。  
  
 次の表は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] が備えているデータ処理拡張機能を示しています。  
  
|データ処理拡張機能|説明|  
|-------------------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 向けデータ処理拡張機能|.NET Framework Data Provider for SQL Server を使用して [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]と接続し、データを取得します。|  
|OLE DB 向けデータ処理拡張機能|.NET Framework Data Provider for OLE DB を使用します。 この拡張機能を使用して、レポート サーバーは、OLE DB プロバイダーを持つすべてのデータ ソースをクエリできます。|  
|Oracle 向けデータ処理拡張機能|.NET Framework Data Provider for Oracle を使用します。 この拡張機能を使用して、レポート サーバーは、Oracle クライアント接続ソフトウェアをとおして Oracle データ ソースにアクセスできます。|  
|ODBC 向けデータ処理拡張機能|.NET Framework Data Provider for ODBC を使用します。 この拡張機能を使用して、レポート サーバーは、ODBC ドライバーが存在するすべてのデータベースのデータにアクセスできます。|  
  
 [!INCLUDE[ssRS](../../../includes/ssrs.md)] データ処理 API を使用して、カスタム データ処理をレポート サーバーに追加できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] には、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] のデータ プロバイダーに対するサポートが組み込まれています。 既に完全なデータ プロバイダーを実装している場合は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能を実装する必要がありません。 ただし、セキュリティで保護された接続の資格情報やサーバー側の集計など、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 2005 に固有の機能を含むようにデータ プロバイダーの拡張を検討してください。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] が備えている各データ処理拡張機能は、共通するインターフェイスのセットを使用します。 これにより、各拡張機能に比較機能が確実に実装されます。  
  
 独自のデータ ソース用のデータ処理拡張機能を開発できます。インターフェイスを使用して、データ処理の層を共通するデータベース インフラストラクチャに追加することもできます。 カスタム データ処理拡張機能を配置して、組織の既存レポート サーバーにデータをシームレスに統合できます。 ユーザーに提供するカスタム レポート スイートの一部として使用することもできます。  
  
 ![データ処理拡張機能のアーキテクチャ](../../../reporting-services/extensions/data-processing/media/bk-dataprocess-extensions.gif "データ処理拡張機能のアーキテクチャ")  
Reporting Services データ処理拡張機能のアーキテクチャ  
  
 カスタム [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能を実装する利点は、次のとおりです。  
  
-   データ アクセス アーキテクチャを簡便化します。多くの場合、メンテナンスがしやすくなり、パフォーマンスが向上します。  
  
-   拡張機能固有の機能をユーザーに直接提示できます。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 内のデータ ソースにユーザーが直接アクセスするための固有のインターフェイスです。  
  
## <a name="data-extension-process-flow"></a>データ拡張機能の処理フロー  
 カスタム データ拡張機能を開発する前に、レポート サーバーがデータ拡張機能を使用してどのようにデータを処理するか理解しておく必要があります。 レポート サーバーによって呼び出されるコンストラクターとメソッドも理解してください。  
  
 ![データ処理拡張機能の処理の流れ](../../../reporting-services/extensions/data-processing/media/bk-ext-01.gif "データ処理拡張機能の処理の流れ")  
レポート サーバーによって呼び出されるデータ拡張機能のステップ バイ ステップ処理フロー  
  
 この図は、次の順序によるイベントを示しています。  
  
1.  レポート サーバーは、接続オブジェクトを作成し、レポートに関連付けられた接続文字列と資格情報を渡します。  
  
2.  レポートのコマンド テキストを使用して、コマンド オブジェクトを作成します。 このプロセスでは、コマンド テキストを解析し、コマンドのパラメーターを作成するコードがデータ処理拡張機能に含まれる場合もあります。  
  
3.  コマンド オブジェクトとパラメーターを処理した後、データ リーダーを生成します。データ リーダーによって、結果セットが返され、レポート サーバーがレポート データをレポート レイアウトに関連付けることができます。  
  
## <a name="developer-requirements"></a>開発者要件  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能を開発するための要件は次のとおりです。  
  
-   レポート デザイナーまたはレポート サーバーがインストールされた配置用コンピューター  
  
-   [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] 以上または [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Software Development Kit (SDK) がインストールされた開発用コンピューター。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の機能についてよく理解していること  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vstecado](../../../includes/vstecado-md.md)] アーキテクチャ、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] データ プロバイダー、ADO.NET DataSet オブジェクト、および共通する [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] インターフェイスについてよく理解していること。  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# や [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET など、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 言語による開発経験があること。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
