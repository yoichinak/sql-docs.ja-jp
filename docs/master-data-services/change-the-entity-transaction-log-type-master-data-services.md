---
description: エンティティのトランザクション ログの種類の変更 (マスター データ サービス)
title: エンティティのトランザクション ログの種類の変更
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 75250b32-3384-43c2-9b5c-1607cc3aa7b3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 693311dcf687c4df6c138f7b881923c05f59da77
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500741"
---
# <a name="change-the-entity-transaction-log-type-master-data-services"></a>エンティティのトランザクション ログの種類の変更 (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  エンティティのトランザクション ログの種類を、"属性"、"メンバー"、または "なし" に変更できます。  
  
|[トランザクション ログの種類]|説明|  
|--------------------------|-----------------|  
|属性|エンティティの変更ログは、属性レベルで保存されます。<br /><br /> トランザクションログは、の場合と同様に保存され [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ます。|  
|メンバー|エンティティの変更ログは、行レベルで保存されます。<br /><br /> すべての属性の変更に対し、新しい行の更新がトリガーされます。<br /><br /> トランザクション ログの種類として "行" を使用している場合、エンティティは、緩やかに変化するディメンション タイプ 4 として保存されます。 タイプ 2 のサブスクリプション ビューとタイプ 4 の (履歴) サブスクリプション ビューがサポートされます。 詳細については、「[サブスクリプション ビュー形式 (マスター データ サービス)](../master-data-services/subscription-view-formats-master-data-services.md)」を参照してください。<br /><br /> より優れたパフォーマンスが得られます。|  
|None|変更ログは保存されません。<br /><br /> 最適なパフォーマンスが得られます。|  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [システム管理] 機能領域にアクセスする権限が必要です。詳細については、「[機能領域権限 (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   エンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
 **トランザクション ログの種類を変更するには**  
  
1.  マスター データ マネージャーで、 **[システム管理]** をクリックします。  
  
2.  **[モデルの管理]** ページで、編集するエンティティのモデルの行を選択し、 **[エンティティ]** をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、更新するエンティティの行を選択し、 **[編集]** をクリックします。  
  
4.  ドロップダウン リストでトランザクション ログの種類を選択します。  
  
5.  **[保存]** をクリックします。  
  
  
