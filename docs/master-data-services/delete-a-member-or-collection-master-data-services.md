---
description: メンバーまたはコレクションを削除する (マスター データ サービス)
title: メンバーまたはコレクションを削除する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c7245b06b114c62b7fd0dde543f8a7a2859bd842
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500639"
---
# <a name="delete-a-member-or-collection-master-data-services"></a>メンバーまたはコレクションを削除する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で、不要になったメンバーまたはコレクションを削除します。 複数のメンバーを一括で削除する場合は、代わりにステージング テーブルを使用します。 詳細については、「[テーブルからのデータのインポート &#40;マスターデータサービス](../master-data-services/import-data-from-tables-master-data-services.md)」を参照してください&#41;  
  
> [!NOTE]  
>  別のメンバーのドメイン ベースの属性値として使用されているメンバーは削除できません。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   メンバーの場合は、メンバーを削除するリーフ モデル オブジェクトに対する **削除** 権限が最低限必要です。  
  
-   コレクションの場合は、削除するリーフ コレクション オブジェクトに対する **更新** 権限が最低限必要です。  
  
### <a name="to-delete-a-member-or-collection"></a>メンバーまたはコレクションを削除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  次の操作を実行します。  
  
    -   リーフ メンバーを削除するには、メニュー バーの **[エンティティ]** をポイントして、メンバーを含むエンティティの名前をクリックします。  
  
    -   統合メンバーを削除するには、メニュー バーの **[階層]** をポイントして、メンバーを含む階層の名前をクリックします。 階層内で、メンバーが含まれているノードをクリックします。  
  
    -   コレクションを削除するには、メニュー バーの **[コレクション]** をポイントして、コレクションを含むエンティティの名前をクリックします。  
  
5.  グリッドで、削除するメンバーまたはコレクションの行をクリックします。  
  
6.  **[メンバーの削除]**、 **[削除]**、または **[コレクションの削除]** をクリックします。  
  
7.  エンティティ管理者には、エンティティ バージョンで論理削除されたすべてのメンバーを消去 (物理削除) するメニュー オプションも表示されます。  
  
8.  確認のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [メンバーまたはコレクションを再アクティブ化する &#40;マスターデータサービス&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [メンバー &#40;マスターデータサービス&#41;](../master-data-services/members-master-data-services.md)   
 [コレクション (マスター データ サービス)](../master-data-services/collections-master-data-services.md)  
  
  
