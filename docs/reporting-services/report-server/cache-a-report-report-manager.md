---
title: レポートのキャッシュ (レポート マネージャー) | Microsoft Docs
description: レポート マネージャーでキャッシュされたレポートの有効期限をスケジュールする方法について説明します。 レポートをキャッシュすると、キャッシュに残っていれば、表示速度が上がります。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- cached reports [Reporting Services]
- schedules [Reporting Services], report expiration
- expiration [Reporting Services]
ms.assetid: 723d1cb0-c2e7-4763-8690-a6a7a8bbbb90
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 36bc03b94c42d8cf660039eb04c73ce88cf18223
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934956"
---
# <a name="cache-a-report-report-manager"></a>レポートのキャッシュ (レポート マネージャー)
  パフォーマンスを向上させる方法の 1 つに、レポートのキャッシュ プロパティを構成するという方法があります。 レポートをキャッシュに格納した場合、表示されたレポートのコピーが短時間、保存されます。 レポートを要求した 1 人目のユーザーは、すべての処理が完了しないとレポートを閲覧できませんが、 それ以降、同じレポートを要求したユーザーは、キャッシュの保持時間内であれば、処理が既に完了しているため、すぐにレポートを閲覧できます。  
  
 キャッシュできるレポートの種類には制限があります。 たとえば、レポート出力がユーザー ID によって異なる場合や、レポートを要求したユーザーのセキュリティ トークンを使ってデータが取得される場合、レポートをキャッシュすることはできません。 詳細については、「 [レポートのキャッシュ (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)でキャッシュを事前に読み込む唯一の方法でした。  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>キャッシュされたレポートの有効期限をスケジュールするには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../web-portal-ssrs-native-mode.md) を開始します。  
  
2.  レポート マネージャーで **[コンテンツ]** ページに移動します。 キャッシュ プロパティを設定するレポートに移動し、アイテムの上にマウス ポインターを移動して、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[管理]** をクリックします。  
  
4.  左フレームの **[処理オプション]** をクリックします。  
  
5.  このページで、 **[常に最新データを使用して、このレポートを実行する]** を選択します。  
  
6.  次の 2 つのキャッシュ オプションのいずれかを選択し、以下のように有効期限を構成します。  
  
    -   キャッシュされたコピーが、特定の期間が過ぎた後で有効期限が切れるように構成するには、 **[レポートの一時コピーをキャッシュします。レポートのコピーの有効期限は数分後に切れます**。 レポートの有効期限を分単位で入力します。  
  
    -   キャッシュされたコピーが、スケジュールに基づいて有効期限が切れるように構成するには、 **[レポートの一時コピーをキャッシュします。次のスケジュールでレポートのコピーの有効期限は切れます。]** をクリックします。 **[構成]** をクリックするか、レポートの有効期限を制御する共有スケジュールを選択します。  
  
7.  **[Apply]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   
 [レポートのキャッシュ (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)  
  
