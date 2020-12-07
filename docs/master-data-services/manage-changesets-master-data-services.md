---
description: 変更セットの管理 (マスター データ サービス)
title: 変更セットの管理
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cc74d46d-7566-45d8-9b51-2cfc262f6abe
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 852396b6c3eb77141e964f1ba72d141153a0badb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471916"
---
# <a name="manage-changesets-master-data-services"></a>変更セットの管理 (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で、すべての変更をモデルとバージョンごとに管理できます。  
  
## <a name="prerequisites"></a>[前提条件]  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。 詳細については、「 [機能領域のアクセス許可 &#40;マスターデータサービス&#41;](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   少なくとも、エンティティまたはその属性のいずれかに対する読み取りアクセス権が必要です。  
  
-   エンティティ管理者の場合は、自分が作成した変更セットと、承認のために保留になっている変更セットを管理できます。  
  
-   エンティティ管理者でない場合は、自分が作成した変更セットのみを管理できます。  
  
## <a name="to-manage-the-changesets"></a>変更セットを管理するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[変更セット]** をクリックします。 選択したモデルとバージョンで管理できるすべての変更セットが表示されます。  
  
3.  変更セットの詳細を表示するには、 **[適用]** をクリックします。  
  
4.  変更セットを削除するには、 **[削除]** をクリックします。 削除できるのは、状態が保留中または承認済み以外の変更セットだけです。  
  
5.  変更セットを追加するには、 **[追加]** をクリックします。  
  
6.  変更セットを編集するには、 **[編集]** をクリックします。  
  
  
