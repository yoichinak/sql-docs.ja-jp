---
title: モデル配置パッケージを配置する (MDSModelDeploy)
description: MDSModelDeploy を使用してマスターデータサービスでパッケージを展開する方法について説明します。 パッケージには、モデルオブジェクトのみ、またはモデルオブジェクトとデータのどちらかを含めることができます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ade6b388deb6414a6b2940d5fef74a9f26ef4637
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100350211"
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>MDSModelDeploy を使用したモデルの配置パッケージの配置

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、MDSModelDeploy ツールを使用して、次のどちらかを含むパッケージを配置します。  
  
-   モデル オブジェクトのみ。  
  
-   モデル オブジェクトとデータ。  
  
 モデル オブジェクトのみを含むパッケージを配置する必要がある場合は、代わりに、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションのモデル配置ウィザードを使用できます。 詳細については、「 [ウィザードを使用したモデルの配置パッケージの展開](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)」を参照してください。  
  
> [!IMPORTANT]  
>  パッケージは、そのパッケージが作成されたエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にのみ配置できます。 つまり、 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] で作成されたパッケージを [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 以降に配置することはできません。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   ターゲット **環境の** [システム管理] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 機能領域にアクセスする権限が必要です。  
  
-   モデルの配置パッケージが必要です。 詳細については、「  [MDSModelDeploy を使用したモデルの配置パッケージの作成](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)」を参照してください。  
  
-   モデルを配置する環境の管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   データを使用してモデルを更新する場合、配置先のバージョンを **ロック** または **コミット** することはできません。  
  
### <a name="to-deploy-a-model-deployment-package"></a>モデルの配置パッケージを配置するには  
  
1.  新しいモデルを配置するのか、モデルを複製するのか、以前に複製したモデルを更新するのかを決定します。 詳細については、「[モデル配置オプション (マスター データ サービス)](../master-data-services/model-deployment-options-master-data-services.md)」を参照してください。  
  
2.  管理者のコマンド プロンプトを開き、MDSModelDeploy.exe のある場所に移動します。  
  
    -   MDS を既定の場所にインストールした場合、ツールは *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration にあります。  
  
    -   MDS を既定の場所にインストールしなかった場合は、ローカル コンピューター内で MDSModelDeploy.exe を検索します。  
  
3.  任意。 オプションおよびヘルプを表示します。  
  
    -   使用可能なすべてのオプションを表示するには、「 `MDSModelDeploy` 」と入力し、Enter キーを押します。  
  
    -   オプションのヘルプを表示するには、「 *」と入力します。* OptionName `MDSModelDeploy help OptionName`はオプションの名前です。  
  
4.  任意。 Web アプリケーションが複数ある場合、次のコマンドを入力し、Enter キーを押して、配置するサービスの名前を確認します。  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     値の一覧が返されます (例: `MDS1, Default Web Site, MDS`)。 モデルを配置するには、この一覧の最初の値 (この例では、 `MDS1`) が必要です。  
  
5.  モデルを配置するのか、モデルを複製するのか、以前に複製したモデルを更新するのかに応じて、コマンド プロンプトに次のコマンドを入力し、Enter キーを押します。  
  
    -   新しいモデルを作成するには  
  
        ```  
        MDSModelDeploy deploynew -package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   モデルの複製を作成するには  
  
        ```  
        MDSModelDeploy deployclone -package PackageName  
        ```  
  
    -   既存のモデルとそのデータを更新するには  
  
        ```  
        MDSModelDeploy deployupdate -package PackageName -version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  MDSModelDeploy ツールを使用して既存のモデルとそのデータを更新するときに、配置先モデルに存在するエンティティ、属性、またはメンバーがパッケージに含まれていない場合は、MDSModelDeploy によって、そのエンティティ、属性、またはメンバーがモデルから削除されることはありません。  
  
     *PackageName* はパッケージ (.pkg) ファイルの名前、 *ModelName* は新しいモデルの名前、 *VersionName* はバージョンの名前、 *ServiceName* は前の手順で返されたサービスの名前です。 モデル名とバージョン名は大文字と小文字の違いも含めて正確に指定してください。  
  
6.  パッケージが正常に配置されると、"MDSModelDeploy 操作は正常に完了しました" というメッセージが表示されます。  
  
 **注:**  
  
-   パッケージ内のサブスクリプション ビューの名前が、既存のモデル内のサブスクリプション ビューの名前と同じである場合、この警告は " **配置機能サブスクリプション ビューが名前変更されました** " と表示され、このビューは *modelname.subscriptionviewname* という名前で作成されます。 この名前が既に使用されている場合、サブスクリプション ビューは作成されません。  
  
-   配置プロセスには、次の 4 つの手順があります。  
  
    1.  モデル オブジェクトが作成されます。  
  
    2.  ビジネス ルールが作成されます。  
  
    3.  サブスクリプション ビューが作成されます。  
  
    4.  マスター データが設定されます。  
  
-   新しいモデルまたは複製モデルを作成する場合、いずれかの手順の実行中にプロセスが失敗すると、モデルは削除されます。  
  
     モデルを更新する場合、最初の 3 つの手順の実行中にプロセスが失敗すると、そのプロセスは続行されません。ただし、既に行われた変更はロールバックされません。 手順 4. でプロセスが失敗すると、更新可能なメンバーが更新されます。  
  
## <a name="next-steps"></a>次の手順  
 ファイル属性、ユーザーとグループの権限は、モデル配置パッケージに含まれていません。 モデルを配置した後、これらを手動で更新する必要があります。 詳細については、次を参照してください:  
  
-   [モデル オブジェクト権限を割り当てる (マスター データ サービス)](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [モデルの配置 (マスター データ サービス)](../master-data-services/deploying-models-master-data-services.md)  
  
  
