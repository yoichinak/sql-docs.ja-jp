---
title: レポート履歴を制限する - Reporting Services | Microsoft Docs
description: レポート サーバーのレポート履歴を構成する方法について説明します。 特定のレポートのレポート履歴を構成する方法についても説明します。
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 809d11c82a9b09a23590592ec3f7b433e3c9ca43
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986658"
---
# <a name="limit-report-history---reporting-services"></a>レポート履歴を制限する - Reporting Services
  レポート履歴とは、時間の経過と共に作成されるレポート スナップショットの集まりです。 レポート履歴は必要時に作成できるほか、どの程度の頻度でスナップショットを作成し、レポート履歴に追加するかをスケジュールで設定することもできます。  
  
 レポート履歴は、レポート サーバー データベースに格納されます。 レポート スナップショットに大量のデータが含まれている場合は、スナップショットを保持することによるデータベース サイズへの影響を最小限に抑えるために、レポート履歴を制限することを検討する必要があります。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-history-for-a-report-server"></a>レポート サーバーのレポート履歴を構成するには  
  
1.  レポート マネージャーのグローバル ツール バーで、 **[サイトの設定]** をクリックします。  
  
2.  すべてのレポート履歴を制限なく保持する場合は、 **[レポート履歴に無制限の数のスナップショットを保持する]** を選択します。 それ以外の場合は、 **[レポート履歴のコピーの数を制限する]** を選択し、特定のレポートに対して保持できるスナップショットの最大数を指定します。  
  
3.  **[Apply]** をクリックします。  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>特定のレポートのレポート履歴を構成するには  
  
1.  レポート マネージャーで、履歴を構成するレポートに移動し、そのレポートをクリックして開きます。  
  
2.  **[プロパティ]** タブをクリックします。  
  
3.  **[履歴]** タブをクリックします。  
  
4.  レポートのオプションを選択し、 **[適用]** をクリックします。 各オプションに関する詳細については、「[[スナップショット オプション] プロパティ ページ &#40;レポート マネージャー&#41;](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130))」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポート履歴へのスナップショットの追加 &#40;レポート マネージャー&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../web-portal-ssrs-native-mode.md)  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="to-configure-report-history-for-a-report-server"></a>レポート サーバーのレポート履歴を構成するには  
  
1.  Web ポータルのグローバル ツール バーで、 **[サイトの設定]** をクリックします。  
  
2.  すべてのレポート履歴を制限なく保持する場合は、 **[レポート履歴に無制限の数のスナップショットを保持する]** を選択します。 それ以外の場合は、 **[レポート履歴のコピーの数を制限する]** を選択し、特定のレポートに対して保持できるスナップショットの最大数を指定します。  
  
3.  **[Apply]** をクリックします。  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>特定のレポートのレポート履歴を構成するには  
  
1.  Web ポータルで、履歴を構成するレポートに移動し、そのレポートをクリックして開きます。  
  
2.  **[プロパティ]** タブをクリックします。  
  
3.  **[履歴]** タブをクリックします。  
  
4.  レポートのオプションを選択し、 **[適用]** をクリックします。 各オプションに関する詳細については、「[[スナップショット オプション] プロパティ ページ](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130))」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポート履歴にスナップショットを追加するレポート履歴にスナップショットを追加する](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   

::: moniker-end
