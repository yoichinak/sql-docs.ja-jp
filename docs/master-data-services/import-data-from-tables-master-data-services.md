---
title: テーブルからのデータのインポート
description: テーブルからデータをインポートし、モデルのデータを一括で変更します。 マスターデータサービスデータベースのデータを追加、更新、および削除するには、次の手順に従います。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ad5b83b1-8e40-4ef8-9ba8-4ea17a58b672
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f4b7f610ca23940c676befc107331b406c124cb2
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92197026"
---
# <a name="import-data-from-tables-master-data-services"></a>テーブルからのデータのインポート (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]のモデルに一括でデータの追加および変更を行えます。  
  
 **前提条件**  
  
-   Stg にデータを挿入する権限が必要です。 \<name>_Leaf、stg。 \<name>_Consolidated、stg。 \<name>データベースのテーブルを _Relationship [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] します。  
  
-   \<name>データベースで stg.udp_ _Leaf、stg udp \_ \<name> _Consolidated、または stg. udp \_ \<name> _Relationship ストアドプロシージャ [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] のいずれかを実行する権限が必要です。  
  
-   モデルのステータスが **[コミット済み]** でないことが必須です。  
  
 **データベースのデータを追加、更新、および削除するには [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]**  
  
1.  必須フィールドの値を指定するなど、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの適切なステージング テーブルにインポートするメンバーを準備します。 ステージング テーブルの概要については、「[概要: テーブルからのデータのインポート (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)」を参照してください。  
  
    -   リーフメンバーの場合、テーブルは stg です。 \<name>_Leaf。ここでは、 \<name> 対応するエンティティを参照します。 必須フィールドの詳細については、「[リーフ メンバー ステージング テーブル (マスター データ サービス)](../master-data-services/leaf-member-staging-table-master-data-services.md)」を参照してください。  
  
    -   統合メンバーの場合、テーブルは stg です。 \<name>_Consolidated。 必須フィールドの詳細については、「[統合メンバー ステージング テーブル (マスター データ サービス)](../master-data-services/consolidated-member-staging-table-master-data-services.md)」を参照してください。  
  
    -   明示的階層内のメンバーの位置を移動する場合、テーブルは stg です。 \<name>_Relationship。 必須フィールドの詳細については、「[リレーションシップ ステージング テーブル (マスター データ サービス)](../master-data-services/relationship-staging-table-master-data-services.md)」を参照してください。  
  
         明示的階層内のメンバーの移動の概要については、「[概要: テーブルからのデータのインポート (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)」を参照してください。  
  
    -   **[ImportType]** フィールドの値を使用して、メンバーの新規作成、メンバーの非アクティブ化、またはメンバーの削除を行っていることを指定します。 値の詳細については、「[リーフ メンバー ステージング テーブル (マスター データ サービス)](../master-data-services/leaf-member-staging-table-master-data-services.md)」および「[統合メンバー ステージング テーブル (マスター データ サービス)](../master-data-services/consolidated-member-staging-table-master-data-services.md)」を参照してください。  
  
         メンバーの非アクティブ化と削除の概要については、「[概要: テーブルからのデータのインポート (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)」を参照してください。  
  
2.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースのデータベース エンジン インスタンスに接続します。  
  
     詳細については、「 [SQL Server Management Studio](../ssms/sql-server-management-studio-ssms.md)」を参照してください。  
  
3.  [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインポートおよびエクスポート] ウィザードを使用して、データをステージング テーブルにインポートします。  
  
     詳細については、「 [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)」を参照してください。  
  
4.  次のいずれかを実行して、ステージング テーブルからデータを [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] テーブルに読み込みます。  
  
    -   データの移動先のステージング テーブルに対応するステージング ストアド プロシージャを実行します。  
  
         ステージング ストアド プロシージャとステージング テーブルの概要については、「[概要: テーブルからのデータのインポート (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)」を参照してください。 ステージング ストアド プロシージャのパラメーターの詳細およびコード例については、「[ステージング ストアド プロシージャ (マスター データ サービス)](../master-data-services/staging-stored-procedure-master-data-services.md)」を参照してください。  
  
    -   マスター データ管理の **[統合管理]** 機能領域 を使用します。  
  
         **[ステージング バッチ]** ページで、ドロップダウン リストでデータの追加先のモデルを選択してから、 **[バッチの開始]** をクリックします。 バッチ処理の状態が、 **[状態]** フィールドに示されます。 状態の詳細については、「[インポート状態 (マスター データ サービス)](../master-data-services/import-statuses-master-data-services.md)」を参照してください。  
  
         ![マスター データ マネージャーでの [ステージング バッチ] ページ](../master-data-services/media/mds-stagingbatchespage.png "マスター データ マネージャーでの [ステージング バッチ] ページ")  
  
         ステージング処理は、 **の** [ステージング バッチの間隔] [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]設定に定められた間隔で開始されます。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
5.  ステージング中に発生したエラーを表示します。 詳細については、「[ステージング中に発生したエラーの表示 (マスター データ サービス)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)」および「[ステージング処理のエラー (マスター データ サービス)](../master-data-services/staging-process-errors-master-data-services.md)」を参照してください。  
  
6.  ビジネス ルールに対してデータを検証します。  
  
     マスター データ マネージャーで、モデルの **[エクスプ ローラー]** 機能領域に移動してから、データを検証するビジネス ルールを適用します。 詳細については、「[ビジネス ルールに対して特定のメンバーを検証する (マスター データ サービス)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)」を参照してください。 データの検証にはストアド プロシージャを使用することもできます。 詳細については、「 [検証ストアド プロシージャ (マスター データ サービス)](../master-data-services/validation-stored-procedure-master-data-services.md)」を参照してください。  
  
     ステージング テーブルからデータを読み込む場合、ビジネス ルールに対してデータが自動的に検証されることはありません。 検証とその実施タイミングの詳細については、「[検証 (マスター データ サービス)](../master-data-services/validation-master-data-services.md)」を参照してください。  
  
