---
description: 属性の型の変更 (Excel 用 MDS アドイン)
title: 属性の型の変更
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1fd0e7f0acbe6792a5d303d50ef66014ebc5c1cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257571"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>属性の型の変更 (Excel 用 MDS アドイン)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]では、許可される文字のデータ型または文字数が間違っている場合に、管理者が属性の型を変更することができます。  
  
 属性の型を変更して制約リスト (ドメイン ベースの属性) を作成する場合は、「[ドメイン ベースの属性を作成する (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)」を参照してください。  
  
> [!NOTE]  
>  **[名前]** 列または **[コード]** 列の型または長さを更新することはできません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[システム管理]** および **[エクスプローラー]** 機能領域に対する権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   既存のモデル、エンティティ、および属性が存在している必要があります。  
  
### <a name="to-change-the-attribute-type"></a>属性の型を変更するには  
  
1.  Excel で、変更する列 (属性) を含むエンティティを読み込みます。 詳細については、「 [マスター データ サービスからデータを Excel にエクスポート](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)」を参照してください。  
  
2.  変更する列の任意のセルをクリックします。  
  
3.  **[モデルの構築]** グループの **[属性プロパティ]** をクリックします。  
  
4.  **[属性プロパティ]** ダイアログ ボックスで、必要に応じて設定を更新します。  
  
5.  **[OK]** をクリックします。  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>属性の型を変更したときに実行される動作  
 属性が任意の MDS ビジネス ルールまたは派生階層によって参照されるなど、属性に関する依存関係が存在する場合、属性のデータ型を変更できません。 オブジェクトによって参照されているため属性の型を変更できないことを示すエラー メッセージが表示されます。  
  
 属性値のデータ型の変換中にエラーが発生した場合、MDS は次のことを実行します。  
  
-   属性のデータ型を変更する。  
  
-   "_old" サフィックスが付いた、前の値が格納された属性のコピーを生成する。 これを、非推奨の属性といいます。  
  
## <a name="see-also"></a>参照  
 [属性 &#40;マスターデータサービス&#41;](../../master-data-services/attributes-master-data-services.md)   
 [モデルの構築 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  
