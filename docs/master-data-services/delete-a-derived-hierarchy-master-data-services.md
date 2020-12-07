---
description: 派生階層を削除する (マスター データ サービス)
title: 派生階層を削除する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting derived hierarchies [Master Data Services]
- derived hierarchies, deleting
ms.assetid: f46d660e-47f2-47ca-9372-1b5931540beb
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b86680615b5c823d5e1db08860ddbdd5ff52bd80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495055"
---
# <a name="delete-a-derived-hierarchy-master-data-services"></a>派生階層を削除する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、不要になった派生階層を削除します。  
  
> [!NOTE]  
>  派生階層を削除しても、その階層が基づいている属性リレーションシップには影響しません。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-delete-a-derived-hierarchy"></a>派生階層を削除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  メニュー バーの **[管理]** をポイントして **[派生階層]** をクリックします。  
  
3.  **[派生階層のメンテナンス]** ページの **[モデル]** の一覧からモデルを選択します。  
  
4.  削除する派生階層の行を選択します。  
  
5.  **[削除]** をクリックします。  
  
6.  確認のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [派生階層 &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [派生階層 (マスター データ サービス)](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
