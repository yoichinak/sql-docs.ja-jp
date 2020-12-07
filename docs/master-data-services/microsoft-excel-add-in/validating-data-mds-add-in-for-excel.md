---
description: データの検証 (Excel 用 MDS アドイン)
title: データの検証
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 71eda98f-01a4-4fff-8246-be3133782523
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b878dcc17cf5ea23b1c5eccca58cdab39cfb7524
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257893"
---
# <a name="validating-data-mds-add-in-for-excel"></a>データの検証 (Excel 用 MDS アドイン)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]でデータをパブリッシュするときに、以下の 2 種類の検証が実行されます。  
  
-   定義されているすべてのビジネス ルールがデータに適用されます。  
  
-   許可されている属性値 (文字数やデータ型など) に対してデータがチェックされます。  
  
 どちらの場合も、有効なデータが MDS リポジトリにパブリッシュされます。 無効なデータは強調表示され、エラーの詳細は状態列で確認できます。  
  
## <a name="when-validation-occurs"></a>検証が実行されるタイミング  
 では、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 新しいデータまたは変更されたデータをパブリッシュするとき、またはビジネスルールを手動で適用するときに、検証が行われます。  
  
 ビジネス ルールの検証に失敗しても、データは MDS リポジトリにパブリッシュされます。 入力の検証が失敗した場合は、データはリポジトリにパブリッシュされません。  
  
## <a name="validation-statuses"></a>検証状態  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]で考えられる検証状態は、次のとおりです。  
  
 その他の状態については、「[検証状態 (マスター データ サービス)](../../master-data-services/validation-statuses-master-data-services.md)」を参照してください。  
  
|Status|説明|  
|------------|-----------------|  
|検証に失敗しました|行内の 1 つ以上の値で、MDS 管理者によって定義されたビジネス ルールに対する検証が失敗しました。|  
|検証に成功しました|行内のすべての値は、ビジネス ルールに対する検証にパスしました。|  
  
## <a name="input-statuses"></a>入力状態  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]で考えられる入力状態は、次のとおりです。  
  
|Status|説明|  
|------------|-----------------|  
|エラー|行内の 1 つまたは複数の値が、長さやデータ型などのシステム要件を満たしていません。 MDS リポジトリ内の値は更新されません。|  
|新しい行|行内の値は、まだ MDS リポジトリにパブリッシュされていません。|  
|[読み取り専用]|ログインしているユーザーは、行内の 1 つ以上の値に対して読み取り専用の権限を持っていて、値は更新されません。|  
|変更なし|行の値は、ワークシート内で変更されていません。 これは、リポジトリ内の値が変更されていないという意味ではありません。シート内の最新のデータを取得するには、 **[接続と読み込み]** グループで、 **[読み込みまたは更新]** をクリックします。<br /><br /> これは、各行の既定の設定です。|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|定義されているビジネス ルールで失敗する値を決定します。|[ビジネス ルールの適用 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
|検証エラーを修正するために、メンバーに対して実行されたすべてのトランザクションを確認します。|[メンバーのすべての注釈またはトランザクションの表示 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [概要: Excel からのデータのインポート (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
