---
description: メンバー リビジョン履歴のロールバック (マスター データ サービス)
title: メンバー リビジョン履歴のロールバック
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ec99fc4d464037b4051da46e293efb4b2fb6969a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100355286"
---
# <a name="rollback-member-revision-history-master-data-services"></a>メンバー リビジョン履歴のロールバック (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  メンバー リビジョン履歴は、メンバーが変更されるたびに記録されます。 メンバー リビジョン履歴は前のバージョンにロールバックすることができます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
  
-   選択したメンバーの少なくとも 1 つの属性を更新できるアクセス許可が必要です。 リビジョン履歴をロールバックすると、更新できるすべての属性値が前のバージョンの値にロールバックされます。  
  
-   リビジョン履歴は、エンティティのトランザクション ログの種類がメンバーである場合にのみ使用できます。  
  
 **メンバー リビジョン履歴をロールバックするには**  
  
1.  マスター データ マネージャーで、[エクスプローラー] をクリックします。  
  
2.  ロールバックするエンティティとメンバーを選択します。  
  
3.  **[履歴の表示]** をクリックします。  
  
4.  ロールバックするリビジョンを選択し、 **[ロールバック]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [メンバーリビジョン履歴 &#40;マスターデータサービス&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [エンティティのトランザクション ログの種類の変更 (マスター データ サービス)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  
