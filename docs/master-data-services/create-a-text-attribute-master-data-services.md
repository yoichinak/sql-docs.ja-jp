---
description: テキスト属性を作成する (マスター データ サービス)
title: テキスト属性を作成する
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating text attributes
- creating text attributes [Master Data Services]
ms.assetid: cd8b57de-364d-42a3-9273-c1c6b992bb40
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 687ddace7463aadc9189c6fc7e60566ddc45ed6c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100272593"
---
# <a name="create-a-text-attribute-master-data-services"></a>テキスト属性を作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、ユーザーに属性値としてテキスト文字列を入力させる場合、テキスト属性を作成します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   属性を作成するエンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
## <a name="attribute-information"></a>属性情報  
 作成された属性ごとに、7 列の行がグリッドに追加されます。 次の表で各列について説明します。  
  
|Column|説明|  
|------------|-----------------|  
|Status|属性の状態。<br /><br /> [保存] をクリックすると、属性が更新中であることを示す ![更新状態の画像のアイコン](../master-data-services/media/mds-statusicon-updating.png "状態を更新するためのアイコン") が表示されます。<br /><br /> 属性の作成時または編集時にエラーが発生した場合は、 ![エラー状態の画像のアイコン](../master-data-services/media/mds-statusicon-error.png "エラー状態のアイコン") が表示されます。<br /><br /> それ以外の場合、状態は [OK] になり、 ![[OK] 状態の画像のアイコン](../master-data-services/media/mds-statusicon-ok.png "OK 状態のアイコン") が表示されます。|  
|名前|属性名。|  
|表示名|属性の表示名。|  
|説明|属性の説明。|  
|ピクセル幅の表示|属性の幅。|  
|種類とプロパティ|属性の種類とデータ型の情報。|  
|変更の追跡を有効化|変更の追跡に対して属性が有効になっているかどうかを指定し、グループ番号を括弧で表示します。|  
  
 属性をクリックすると、次の情報が表示されます。  
  
-   **作成者**: 属性を作成したユーザーの名前。  
  
-   **作成日時**: 属性が作成された日時。  
  
-   **更新者**: 属性を最後に更新したユーザーの名前。  
  
-   **更新日時**: 属性が最後に更新された日時。  
  
### <a name="to-create-a-text-attribute"></a>テキスト属性を作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  [ **モデルの管理** ] ページで、グリッドからモデルを選択し、[ **エンティティ**] をクリックします。  
  
3.  **[エンティティの管理]** ページで、属性を作成するエンティティの行を選択します。  
  
4.  **[属性]** をクリックします。  
  
5.  **[属性の管理]** ページで、次のいずれかの操作を行い、 **[追加]** をクリックします。  
  
    -   属性の対象がリーフ メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[リーフ]** を選択します。  
  
    -   属性の対象が統合メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[統合]** を選択します。  
  
    -   属性の対象がコレクションの場合、 **[メンバーの種類]** ボックスの一覧から **[コレクション]** を選択します。  
  
6.  **[名前]** ボックスに属性の名前を入力します。 属性名として使用しない単語の一覧については、「 [予約語 &#40;マスターデータサービス&#41;](../master-data-services/reserved-words-master-data-services.md)」を参照してください。  
  
7.  (省略可能) 表示名を入力し、 **[説明]** ボックスに説明を入力します。  
  
8.  **[ピクセル幅の表示]** ボックスに、 **[エクスプローラー]** グリッドに表示する属性列の幅を入力します。  
  
9. **[属性の種類]** リストから、 **[自由形式]** を選択します。  
  
10. **[データ型]** ボックスの一覧から **[Text]** を選択します。  
  
11. **[長さ]** ボックスに、許可する文字の最大数を入力します。  
  
12. 必要に応じて、 **[変更の追跡を有効化]** を選択して、属性のグループに対する変更を追跡します。 詳細については、「[変更の追跡グループに属性を追加する方法 (マスター データ サービス)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)」を参照してください。  
  
13. **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [属性 &#40;マスターデータサービス&#41;](../master-data-services/attributes-master-data-services.md)   
 [属性名とデータ型 &#40;マスターデータサービスに変更&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Domain-Based 属性 &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [ファイル属性を作成する (マスター データ サービス)](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
