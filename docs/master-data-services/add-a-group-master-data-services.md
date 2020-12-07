---
description: グループを追加する (マスター データ サービス)
title: グループを追加する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- groups [Master Data Services], adding
- adding groups [Master Data Services]
ms.assetid: c7a88381-3b2c-4af7-9cf7-3a930c1abdee
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2a5693bfcc62beaad8f5423d6e5d3dbee5cd7fb7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491514"
---
# <a name="add-a-group-master-data-services"></a>グループを追加する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  **で** [グループ] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ボックスの一覧にグループを追加して、Web アプリケーションに権限を割り当てるプロセスを開始します。 グループ内のユーザーが [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]にアクセスできるようにするには、グループの権限を 1 つまたは複数の機能領域およびモデル オブジェクトに付与する必要があります。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   **[ユーザー/グループの権限]** 機能領域にアクセスするための権限が必要です。  
  
### <a name="to-add-a-group"></a>グループを追加するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[ユーザー/グループの権限]** をクリックします。  
  
2.  **[ユーザー]** ページでメニュー バーから **[グループの管理]** をクリックします。  
  
3.  **[グループの追加]** をクリックします。  
  
4.  グループの名前を Active Directory ドメイン名またはサーバー コンピューターの名前の後に入力します ( *domain\group_name* または *computer\group_name*のように入力します)。  
  
5.  必要に応じて、 **[名前の確認]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
    > [!NOTE]  
    >  ユーザーが最初に [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]にアクセスしたときに、そのユーザーの名前が [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ユーザー一覧に追加されます。  
  
## <a name="next-steps"></a>次の手順  
  
-   [機能領域の権限を割り当てる (マスター データ サービス)](../master-data-services/assign-functional-area-permissions-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [セキュリティ (マスター データ サービス)](../master-data-services/security-master-data-services.md)  
  
  
