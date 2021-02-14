---
title: リーフ メンバー ステージング テーブル
description: リーフメンバーを作成、更新、非アクティブ化、および削除するには、マスターデータサービスデータベースのリーフメンバーステージングテーブルを使用します。
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members staging table [Master Data Services]
- database [Master Data Services], members staging table
ms.assetid: a8c953da-ec20-47dc-8656-ed5f0dfed89b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e38a38d14551b819db0e6ff7f8558448040a7049
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100338228"
---
# <a name="leaf-member-staging-table-master-data-services"></a>リーフ メンバー ステージング テーブル (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースのリーフ メンバー ステージング テーブル (stg.name_Leaf) を使用して、リーフ メンバーを作成、更新、非アクティブ化、および削除します。 また、このテーブルを使用して、リーフ メンバーの属性値を更新できます。  
  
##  <a name="table-columns"></a><a name="TableColumns"></a> テーブルの列  
 次の表は、リーフ ステージング テーブルの各フィールドの用途を説明しています。  
  
|列名|説明|値|  
|-----------------|-----------------|------------|  
|**ID**|自動的に割り当てられる ID。|このフィールドには値を入力しないでください。 バッチが未処理の場合、このフィールドは空白です。|  
|**ImportType**<br /><br /> 必須|ステージング データが [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに既に存在するデータと一致する場合の処理を決定します。|**0**: 新しいメンバーを作成します。 既存の MDS データをステージング データに置き換えます。ただし、ステージング データが NULL の場合は除きます。 NULL 値は無視されます。 文字列の属性値を NULL に変更するには、 **~NULL~** を設定します。 数値の属性値を NULL に変更するには、 **-98765432101234567890** に設定します。 DateTime 型の属性値を NULL に変更するには、 **5555-11-22T12:34:56** に設定します。<br /><br /> **1**: 新しいメンバーのみを作成します。 既存の MDS データに対する更新はすべて失敗します。<br /><br /> **2**: 新しいメンバーを作成します。 既存の MDS データをステージング データに置き換えます。 NULL 値をインポートする場合、既存の MDS 値が上書きされます。<br /><br /> **3**: コード値に基づいて、メンバーを非アクティブにします。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションは維持されますが、UI では利用できなくなります。 メンバーが別のメンバーのドメイン ベースの属性値として使用されている場合、非アクティブ化は失敗します。 代わりの方法については **ImportType5** を参照してください。<br /><br /> **4**: コード値に基づいて、メンバーを完全に削除します。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションが、完全に削除されます。 メンバーが別のメンバーのドメイン ベースの属性値として使用されている場合、削除は失敗します。 代わりの方法については **ImportType6** を参照してください。<br /><br /> **5**: **コード** 値に基づいて、メンバーを非アクティブにします。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションは維持されますが、UI では利用できなくなります。 メンバーが他のメンバーのドメイン ベースの属性値として使用されている場合、関連する値は NULL に設定されます。 ImportType 5 はリーフ メンバー専用です。<br /><br /> **6**: **コード** 値に基づいて、メンバーを完全に削除します。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションが、完全に削除されます。 メンバーが他のメンバーのドメイン ベースの属性値として使用されている場合、関連する値は NULL に設定されます。 ImportType 6 はリーフ メンバー専用です。|  
|**ImportStatus_ID**<br /><br /> 必須|インポート処理の状態。|**0**: レコードがステージング準備済みであることを示すために指定します。<br /><br /> **1**: 自動的に割り当てられ、レコードのステージング処理が正常に完了したことを示します。<br /><br /> **2**: 自動的に割り当てられ、レコードのステージング処理に失敗したことを示します。|  
|**Batch_ID**<br /><br /> Web サービスでのみ必須|ステージング用のレコードをグループ化する、自動的に割り当てられる識別子。 バッチ内のメンバーすべてにこの識別子が割り当てられます。これは、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ユーザー インターフェイスの **[ID]** 列に表示されます。|バッチが未処理の場合、このフィールドは空白です。|  
|**BatchTag**<br /><br /> Web サービス以外は必須|バッチの一意名 (最大 50 文字)。||  
|**ErrorCode**|エラー コードを表示します。 **ImportStatus_ID** が **2** のすべてのレコードについては、「[ステージング処理のエラー (マスター データ サービス)](../master-data-services/staging-process-errors-master-data-services.md)」を参照してください。||  
|**コード**<br /><br /> 必須。**ImportType1** や **2** でコードが自動的に生成される場合は除きます。詳しくは、「[コードの自動作成 (マスター データ サービス)](../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。|メンバーの一意コード。||  
|**名前**<br /><br /> Optional|メンバーの名前。||  
|**NewCode**|メンバー コードを変更する場合にのみ使用します。||  
|\<Attribute name>|エンティティ内の属性ごとに列が存在します。 **ImportType** が **0** または **2** の場合に、これを使用します。 自由形式属性の場合、属性の新しいテキストまたは文字列値を指定します。 ドメイン ベース属性の場合は、属性となるメンバーのコードを指定します。 リンク属性の場合、URL は **https://** で始まる必要があります。<br /><br /> 注: ファイル属性をステージングすることはできません。||  
  
## <a name="see-also"></a>参照  
 [概要: テーブルからのデータのインポート &#40;マスターデータサービス&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [ステージング &#40;マスターデータサービス中に発生したエラーを表示&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [ステージング処理のエラー (マスター データ サービス)](../master-data-services/staging-process-errors-master-data-services.md)  
  
  
