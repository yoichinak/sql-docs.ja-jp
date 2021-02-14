---
description: バージョンをロック解除する (マスター データ サービス)
title: バージョンをロック解除する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- unlocking versions [Master Data Services]
- versions [Master Data Services], unlocking
ms.assetid: b4cf4404-40f3-46fb-801d-cbf80a95448c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fe03c4a0a95462d1dd793eaf82b0c017b3b781e8
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100336226"
---
# <a name="unlock-a-version-master-data-services"></a>バージョンをロック解除する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でモデルのバージョンをロック解除して、モデルのメンバーおよびメンバーの属性に対する変更を有効にします。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   **[バージョン管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   バージョンのステータスは、 **[ロック済み]** である必要があります。 詳細については、「 [バージョンをロックする (マスター データ サービス)](../master-data-services/lock-a-version-master-data-services.md)」を参照してください。  
  
-   [バージョン管理] 機能領域にアクセスする権限が必要です。 詳細については、「 [機能領域のアクセス許可 &#40;マスターデータサービス&#41;](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
### <a name="to-unlock-a-version"></a>バージョンをロック解除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[バージョン管理]** をクリックします。  
  
2.  **[バージョンの管理]** ページで、ロック解除するバージョンの行を選択します。  
  
3.  **[ロックを解除]** をクリックします。  
  
4.  確認のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   [バージョンをロックする (マスター データ サービス)](../master-data-services/lock-a-version-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [バージョン (マスター データ サービス)](../master-data-services/versions-master-data-services.md)  
  
  
