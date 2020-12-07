---
description: ファイル属性を作成する (マスター データ サービス)
title: ファイル属性を作成する
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating file attributes [Master Data Services]
- attributes [Master Data Services], creating file attributes
ms.assetid: d224886b-2ef1-4658-8b01-2213cc4b8df6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cc1b9b6cd36d12e39823cb0915e6fe7b5af4d7bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461863"
---
# <a name="create-a-file-attribute-master-data-services"></a>ファイル属性を作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でファイル属性を作成して、ファイルで属性値を設定します。

## <a name="prerequisites"></a>[前提条件]
 この手順を実行するには

-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。

-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。

-   属性を作成するエンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。

## <a name="attribute-information"></a>属性情報
 作成された属性ごとに、7 列の行がグリッドに追加されます。 次の表で各列について説明します。

|列|説明|
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

### <a name="to-create-a-file-attribute"></a>ファイル属性を作成するには

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

9. **[属性の種類]** リストから、 **[ファイル]** を選択します。

10. **[ファイル拡張子]** ボックスの一覧で、ユーザーがアップロードできるファイルの種類を選択するか、既定値 (*.\*) のままにしてすべてのファイルの種類を許可します。

11. 必要に応じて、 **[変更の追跡を有効化]** を選択して、属性のグループに対する変更を追跡します。 詳細については、「[変更の追跡グループに属性を追加する方法 (マスター データ サービス)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)」を参照してください。

12. **[保存]** をクリックします。

## <a name="see-also"></a>参照
 属性[&#40;マスターデータサービス](../master-data-services/attributes-master-data-services.md)[属性名とデータ &#40;型の変更](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)&#41;マスターデータサービス&#41;[ドメインベースの属性の作成](../master-data-services/create-a-domain-based-attribute-master-data-services.md)&#40;マスターデータサービス&#41;[テキスト属性の作成](../master-data-services/create-a-text-attribute-master-data-services.md)&#40;マスターデータサービス&#41;


