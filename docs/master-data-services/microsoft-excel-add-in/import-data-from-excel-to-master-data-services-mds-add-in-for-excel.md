---
description: Excel からマスター データ サービスにデータをインポートする (Excel 用 MDS アドイン)
title: Excel からのデータのインポート
ms.custom: microsoft-excel-add-in, seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 22d69fafa852007c9642fe641205185115b42175
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100352753"
---
# <a name="import-data-from-excel-to-master-data-services-mds-add-in-for-excel"></a>Excel からマスター データ サービスにデータをインポートする (Excel 用 MDS アドイン)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]で、Excel での作業が終わったときに、変更を保存して他のユーザーがアクセスできるようにするには、MDS リポジトリにデータをパブリッシュします。  
  
> [!NOTE]
>  -   変更をパブリッシュすると、MDS によって管理されるセルのコメントは削除されます。  
> -   MDS によって管理されるセルでは、数式がサポートされていません。 MDS によって管理されるセル内の数式はテキスト値として処理されます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   アクティブなワークシートに MDS によって管理されるデータが含まれており、そのデータに対して変更または追加を行っている必要があります。  
  
-   メンバーを追加する場合、エンティティのコードが自動的に生成されているときは、 **コード** 値を指定する必要はありません。 詳細については、「 [自動コード作成 &#40;マスターデータサービス&#41;](../../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。  
  
### <a name="to-publish-data-to-the-mds-repository"></a>MDS リポジトリにデータをパブリッシュするには  
  
1.  **[パブリッシュと検証]** グループの **[パブリッシュ]** をクリックします。  
  
2.  任意。 **[パブリッシュと注釈設定]** ダイアログ ボックスが表示された場合は、すべての更新で同じ注釈 (コメント) を共有するか、各変更の注釈を個別に設定するかを選択します。  
  
3.  任意。 **[今後、このダイアログ ボックスを表示しない]** チェック ボックスをオンにします。 後で、このダイアログ ボックスが常に表示されるようにするには、 **[設定]** をクリックして **[パブリッシュ時に [パブリッシュと注釈設定] ダイアログ ボックスを表示する]** チェック ボックスをオンにします。  
  
4.  **[発行]** をクリックします。  
  
> [!NOTE]  
>  新しいメンバー (行) をワークシートに追加する場合、MDS リポジトリに正常にパブリッシュできないときは、ワークシートのすべての属性に対する **更新** 権限がない可能性があります。 **[校閲]** タブの **[変更]** グループの **[シート保護の解除]** をクリックし、再度パブリッシュしてください。  
  
## <a name="next-steps"></a>次の手順  
 [ビジネス ルールの適用 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>参照  
 [概要: Excel &#40;Excel 用 MDS アドインからのデータのインポート&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [データの検証 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
  
