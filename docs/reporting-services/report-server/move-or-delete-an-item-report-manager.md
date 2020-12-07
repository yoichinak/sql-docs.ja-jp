---
title: アイテムの移動または削除 (レポート マネージャー) | Microsoft Docs
description: レポート マネージャーのレポート サーバーによって、フォルダーにレポートと関連アイテムが格納されます。 アイテムを移動したり、削除したりできます。 レポート サーバーでは、移動したアイテムへの参照が維持されます。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- moving items
- items [Reporting Services], moving
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c02d85c3230502f3360039b132e8328e40d06d28
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987158"
---
# <a name="move-or-delete-an-item-report-manager"></a>アイテムの移動または削除 (レポート マネージャー)
  レポート サーバーにパブリッシュしたレポートやレポート関連アイテムは、フォルダーに格納されます。 アイテムは異なるフォルダーに移動でき、それらのアイテムへの参照はレポート サーバーによって自動的に保持されます。 アイテムを削除する前に、そのアイテムに依存しているアイテムが他に存在しないか確認してください。  
  
## <a name="move-an-item"></a>アイテムの移動  
 レポート サーバー アイテムは、レポート サーバー フォルダー階層内の異なるフォルダーに移動できます。 アイテムを移動すると、セキュリティ設定などのすべてのプロパティが、アイテムと共に新しい場所に移動します。 フォルダーを移動すると、そのフォルダーに含まれるすべてのアイテムも移動します。  
  
 レポート マネージャーでは、移動できるアイテムがフォルダー階層で示されています。 移動可能な各アイテムのアイコンを次の表に示します。  
  
|アイコン|移動可能なアイテム|  
|----------|-------------------|  
|![Report icon](../../reporting-services/report-server/media/hlp-16doc.gif "レポート アイコン")|レポート|  
|![リンク レポート アイコン](../../reporting-services/report-server/media/hlp-16linked.gif "リンク レポート アイコン")|リンク レポート|  
|![フォルダー アイコン](../../reporting-services/report-server/media/hlp-16folder.gif "フォルダー アイコン")|Folder|  
|![汎用リソース アイコン](../../reporting-services/report-server/media/hlp-16file.gif "汎用リソース アイコン")|汎用リソース|  
|![Shared data source icon](../../reporting-services/report-data/media/hlp-16datasource.png "共有データ ソースのアイコン")|[共有データ ソース]|  
||共有データセット|  
  
 作業に使用するすべてのアイテムを移動できるわけではありません。 サブスクリプションまたはレポート履歴など、レポートに関連付けられたアイテムを移動することはできません。 これらのアイテムは、関連するレポートと共に移動します。 同様に、フォルダー階層の外部にある、共有スケジュールなどのアイテムは移動できません。 操作を行うための権限がない場合は、アイテムを移動できません。 アイテムを移動するための権限は、当該アイテムのロールの割り当てで "レポートの管理"、"モデルの管理"、"フォルダーの管理、および "データ ソースの管理" のタスクを選択した場合に許可されます。  
  
#### <a name="to-move-an-item-from-within-the-contents-page"></a>[コンテンツ] ページでアイテムを移動するには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../web-portal-ssrs-native-mode.md) を開始します。  
  
2.  レポート マネージャーで、 **[コンテンツ]** ページに移動し、移動するアイテムを探します。  
  
3.  アイテムの上にマウス ポインターを移動し、下矢印をクリックします。  
  
4.  ドロップダウン メニューの **[移動]** をクリックします。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  **[場所]** については、アイテムの移動先のフォルダーを指定します。 フォルダーの完全修飾名を入力するか、またはツリー コントロールを使用して目的のフォルダーに移動します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 または、移動するオブジェクトに移動して **[プロパティ]** をクリックし、ページの上部にある **[移動]** をクリックします。  
  
## <a name="delete-an-item"></a>項目を削除する  
 アイテムを削除する前に、そのアイテムが他のアイテムによって使用されていないかどうかを確認してください。 たとえば、共有データ ソースを削除した場合、そのデータ ソースを使用するレポートおよびモデルは実行できなくなります。 レポートを削除すると、そのレポートに関連付けられているサブスクリプションおよびレポート履歴も削除されます。 あるアイテムに依存しているアイテムを検索するには、「[[依存アイテム] ページ &#40;レポート マネージャー&#41;](../web-portal-ssrs-native-mode.md)」を参照してください。  
  
#### <a name="to-delete-a-report-or-item"></a>レポートまたはアイテムを削除するには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../web-portal-ssrs-native-mode.md) を開始します。  
  
2.  レポート マネージャーで、 **[コンテンツ]** ページに移動し、削除するアイテムを探します。  
  
3.  アイテムの上にマウス ポインターを移動し、下矢印をクリックします。  
  
4.  ドロップダウン メニューの **[削除]** をクリックします。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [[コンテンツ] ページ (レポート マネージャー)](/previous-versions/sql/sql-server-2016/ms186470(v=sql.130))   
 [レポートの検索、表示、管理 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
