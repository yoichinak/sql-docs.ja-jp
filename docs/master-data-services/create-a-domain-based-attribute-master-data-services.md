---
description: ドメイン ベースの属性を作成する (マスター データ サービス)
title: ドメイン ベースの属性を作成する
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: daea6bffcefaab4866a27418d48eb2963482a5e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461864"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>ドメイン ベースの属性を作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でドメイン ベースの属性を作成して、属性の値にエンティティのメンバーを設定します。

## <a name="prerequisites"></a>[前提条件]
 この手順を実行するには

-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。

-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。

-   属性値のソースとして使用する 1 つのエンティティが存在する必要があります。 たとえば、Color エンティティに基づくドメイン ベースの属性を作成するには、最初に Color エンティティを作成する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。

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

### <a name="to-create-a-domain-based-attribute"></a>ドメイン ベースの属性を作成するには

1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。

2.  **[モデルの管理]** ページで、モデルをクリックし、 **[エンティティ]** をクリックします。

3.  **[エンティティの管理]** ページで、属性を作成するエンティティの行を選択します。

4.  **[属性]** をクリックします。

5.  **[属性の管理]** ページで、次のいずれかの操作を行い、 **[追加]** をクリックします。

    -   属性の対象がリーフ メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[リーフ]** を選択します。

    -   属性の対象が統合メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[統合]** を選択します。

    -   属性の対象がコレクションの場合、 **[メンバーの種類]** ボックスの一覧から **[コレクション]** を選択します。

6.  **[名前]** ボックスに属性の名前を入力します。 属性名として使用できない単語の一覧については、「[予約語 (マスター データ サービス)](../master-data-services/reserved-words-master-data-services.md)」を参照してください。

7.  任意で、表示名を入力し、 **[説明]** ボックスに説明を入力します。

8.  **[ピクセル幅の表示]** ボックスに、 **[エクスプローラー]** グリッドに表示する属性列の幅を入力します。

9. **[属性の種類]** リストから、 **[ドメイン ベース]** を選択します。

10. **[ドメイン エンティティ]** ボックスの一覧から、属性値を設定するために使用するエンティティを選択します。 

11. **リーフ メンバーのドメイン ベース属性の場合は省略可能。** ドメイン ベース属性の許容値の制約に使用されるフィルターの親属性を選択します。

     フィルターの親属性は、同じエンティティ内で、リーフ メンバーの別のドメイン ベース属性にする必要があります。 派生する階層は、2 つの属性のドメイン エンティティ間の親子関係を定義するレベルで存在する必要があります。

     許容値の制約に関する詳細については、マスター データ サービス ブログの「 [How to filter Domain Based Attribute drop down lists (ドメイン ベース属性のドロップダウン リストをフィルター処理する方法)](https://blogs.msdn.microsoft.com/mds/2015/12/03/in-sql-server-2016-master-data-services-how-to-filter-domain-based-attribute-drop-down-lists/)」を参照してください。

12. **省略可。** **[変更の追跡を有効化]** を選択して、属性のグループに対する変更を追跡します。 詳細については、「[変更の追跡グループに属性を追加する方法 (マスター データ サービス)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)」を参照してください。

13. **[保存]** をクリックします。

## <a name="see-also"></a>参照
 [ドメインベースの属性 &#40;マスターデータサービス](../master-data-services/domain-based-attributes-master-data-services.md)[派生 &#40;階層を作成](../master-data-services/create-a-derived-hierarchy-master-data-services.md)&#41;マスターデータサービス&#41;属性[名とデータ型を変更](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)&#40;マスターデータサービス&#41;[属性 &#40;削除](../master-data-services/delete-an-attribute-master-data-services.md)マスターデータサービス&#41;


