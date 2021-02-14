---
title: エンティティを作成する
description: メンバーとその属性を含むエンティティをマスターデータサービスに作成する方法について説明します。 [システム管理] 領域のアクセス許可が必要です。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8d47a78e4a7e706e91312ee2eb4686121c2b2532
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341432"
---
# <a name="create-an-entity-master-data-services"></a>エンティティを作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でエンティティを作成して、メンバーおよびその属性を含めます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   モデルが存在する必要があります。 詳細については、「[モデルを作成する (マスター データ サービス)](../master-data-services/create-a-model-master-data-services.md)」を参照してください。  
  
### <a name="to-create-an-entity"></a>エンティティを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[Manage Model]** (モデルの管理) ページで、エンティティを作成するモデルをグリッドから選択し、 **[エンティティ]** をクリックします。  
  
3.  **[Manage Entity]** (管理エンティティ) ページで **[追加]** をクリックします。  
  
4.  **[名前]** ボックスに、エンティティの名前を入力します。  
  
5.  必要に応じて、 **[説明]** フィールドに、エンティティの説明を入力します。  
  
6.  必要に応じて、 **[ステージング テーブルの名前]** ボックスに、ステージング テーブルの名前を入力します。  
  
     このフィールドに名前を入力しない場合は、エンティティ名が使用されます。  
  
    > [!TIP]  
    >  ステージング テーブルの名前の一部にはモデル名を使用します。たとえば、 *Modelname_Entityname* のようにします。 こうすることで、データベースからテーブルを見つけやすくなります。 ステージング テーブルの詳細については、「[概要: テーブルからのデータのインポート (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)」を参照してください。
    > [!TIP]
    > ステージング テーブルに既定の名前付けを使用している場合、他のモデルに同じ名前を持つエンティティが存在すると、MDS によってステージング テーブル名に識別子 (例: _1、_2) が自動的に追加されます。
  
7.  **[トランザクション ログの種類]** フィールドで、ドロップダウン リストからトランザクション ログの種類を選択します。  
  
     詳細については、「[エンティティのトランザクション ログの種類の変更 (マスター データ サービス )](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)」を参照してください。  
  
8.  任意。 **[コード値を自動的に作成する]** チェック ボックスをオンにします。 詳細については、「 [自動コード作成 &#40;マスターデータサービス&#41;](../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。  
  
9. 任意。 **[データ圧縮を有効にする]** チェック ボックスをオンします。 既定では、行の圧縮は有効になっています。 詳細については、「 [Data Compression](../relational-databases/data-compression/data-compression.md)」を参照してください。  
  
10. **[保存]** をクリックします。  
  
## <a name="grid-columns"></a>グリッド列  
 作成されたエンティティごとに、13 列の行がグリッドに追加されます。 その列を次に示します。  
  
|名前|説明|  
|----------|-----------------|  
|Status|エンティティの状態。 **[保存]** をクリックすると、エンティティが更新中であることを示す次のイメージが表示されます。<br /><br /> ![状態を更新するためのアイコン](../master-data-services/media/mds-statusicon-updating.png "状態を更新するためのアイコン")<br /><br /> エンティティの作成または編集中にエラーが発生すると、次のイメージが表示されます。<br /><br /> ![エラー状態のアイコン](../master-data-services/media/mds-statusicon-error.png "エラー状態のアイコン")<br /><br /> 適切な状態の場合は、次のイメージが表示されます。<br /><br /> ![OK 状態のアイコン](../master-data-services/media/mds-statusicon-ok.png "OK 状態のアイコン")|  
|name|エンティティ名。|  
|[説明]|エンティティの説明。|  
|ステージング テーブル|データを格納するために使用されるテーブルのプレフィックス名。|  
|[トランザクション ログの種類]|エンティティのトランザクション ログの種類。|  
|コードの自動作成|コードの自動作成が有効かどうかを示します。|  
|データ圧縮|エンティティに対してデータ圧縮が有効かどうかを示します。|  
|同期ターゲット|エンティティが同期関係のターゲットかどうかを示します。|  
|階層が有効|明示的階層に対してエンティティが有効かどうかを示します。 エンティティに対して少なくとも 1 つの明示的階層が作成されている場合は、[はい] になります。|  
|Created By|エンティティを作成したユーザーの名前。|  
|作成日時|エンティティが作成された日付と時刻。|  
|更新者|エンティティを最後に更新したユーザーの名前。|  
|更新日|エンティティが最後に更新された日時。|  
  
## <a name="next-steps"></a>次の手順  
  
-   [テキスト属性を作成する (マスター データ サービス)](../master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [ドメイン ベースの属性を作成する (マスター データ サービス)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [ファイル属性を作成する (マスター データ サービス)](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [エンティティ &#40;マスターデータサービス&#41;](../master-data-services/entities-master-data-services.md)   
 [明示的階層 &#40;マスターデータサービス&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [エンティティ &#40;マスターデータサービスの編集&#41;](../master-data-services/edit-an-entity-master-data-services.md)   
 [エンティティを削除する (マスター データ サービス)](../master-data-services/delete-an-entity-master-data-services.md)  
  
  
