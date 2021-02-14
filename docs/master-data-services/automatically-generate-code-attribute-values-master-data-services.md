---
description: Code 属性の値の自動生成 (Master Data Services)
title: Code 属性の値の自動生成
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 82d501f5d7c5a4a5b79e55571a7351225833680b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341492"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Code 属性の値の自動生成 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、新しいメンバーが作成されるたびに、エンティティの Code 属性の値に整数を自動的に割り当てる場合は、Code 属性の値を自動的に生成します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   エンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
### <a name="to-automatically-generate-code-values"></a>コード値を自動的に生成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデルの管理]** ページで、編集するエンティティが含まれているモデルの行を選択し、 **[エンティティ]** をクリックします。  
  
3.  **[エンティティの管理]** ページで、コードを生成するエンティティの行を選択し、 **[編集]** をクリックします。  
  
4.  **[コード値を自動的に作成する]** チェック ボックスをオンにします。  
  
5.  **[開始]** ボックスに、増分を開始する値を入力します。 メンバーが既に存在する場合は、コードは既存の最も大きい値に基づいて設定されます。 たとえば、最も大きい既存のコード値が 299 の場合、次のメンバーのコード値は 300 に設定されます。  
  
6.  **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [自動コード作成 &#40;マスターデータサービス&#41;](../master-data-services/automatic-code-creation-master-data-services.md)   
 [Code 以外の属性の値の自動生成 (マスター データ サービス)](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
