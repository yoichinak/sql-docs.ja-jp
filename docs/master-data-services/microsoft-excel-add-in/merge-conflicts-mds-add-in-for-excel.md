---
description: 競合のマージ (Excel 用 MDS アドイン)
title: 競合のマージ
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cf95978f-a2c5-4325-8606-dbd4e88741b8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 57b375addf4ef730186f946e17e1b326d54d65e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500575"
---
# <a name="merge-conflicts-mds-add-in-for-excel"></a>競合のマージ (Excel 用 MDS アドイン)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Excel 用の [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] アドインでは、サーバー上でデータが他のユーザーによって変更されている場合、パブリッシュ操作は競合エラーで失敗します。 このエラーを解決するには、競合のマージを実行した後で変更を再パブリッシュします。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   更新するエンティティのリーフ モデル オブジェクトに対する更新権限が最低限必要です。  
  
-   アクティブなワークシートに MDS によって管理されるデータが含まれている必要があります。  
  
-   変更内容を公開しようとしたときに、アクティブなワークシートで競合エラーが発生している必要があります。  
  
### <a name="to-merge-conflicts"></a>競合をマージするには  
  
1.  ワークシートで、競合エラーが発生している行またはセルを選択します。  
  
2.  **[パブリッシュと検証]** メニュー グループの **[競合のマージ]** を選択して **[競合のマージ]** カタログを開きます。  
  
3.  **[競合のマージ]** ダイアログで、次のいずれかの操作を実行できます。  
  
    -   保留中の変更を元に戻し、サーバーから最新のバージョンを再び読み込む場合は、 **[最新]** を選択し、 **[適用]** をクリックします。  
  
    -   ワークシートの元のバージョンを適用する場合は、 **[オリジナル]** を選択し、 **[適用]** をクリックします。  
  
    -   既存のローカルの変更を保持する場合は、 **[このユーザーの変更]** を選択し、 **[適用]** をクリックします。  
  
4.  **[適用]** をクリックした後、さらに変更を加えて、再びパブリッシュすることができます。 または、 **[キャンセル]** をクリックして更新を取り消し、サーバーから最新のバージョンを再び読み込むことができます。  
  
## <a name="see-also"></a>参照  
 [概要: Excel からのデータのインポート (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
