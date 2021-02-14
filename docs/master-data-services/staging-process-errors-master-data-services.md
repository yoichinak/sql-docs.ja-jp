---
title: ステージング処理のエラー
description: この記事では、マスターデータサービスでのステージング処理中に処理されたすべてのレコードに追加されたエラーコードについて説明します。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], error messages
ms.assetid: 0d9be0dd-638f-4dd4-92b2-253fda655455
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 84a5a66cbb8bacb3e1df896fedfa3a051e2f4dbb
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100336269"
---
# <a name="staging-process-errors-master-data-services"></a>ステージング処理のエラー (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  ステージング処理が完了すると、ステージング テーブル内のすべての処理済みレコードの [ErrorCode] 列に値が格納されます。 これらの値を次の表に示します。  
  
|コード|エラー|発生時/詳細|テーブルへの適用|  
|----------|-----------|--------------------------|----------------------|  
|210001|ステージング テーブルに同じメンバー コードが複数回出現します。|ステージング バッチに、同じメンバー コードが複数回含まれます。 メンバーは作成も更新もされません。|Leaf<br /><br /> [統合]<br /><br /> Relationship|  
|210003|属性値は、存在しないメンバーまたは非アクティブなメンバーを参照しています。|ドメイン ベースの属性をステージングするときは、名前ではなく、コードを使用する必要があります。 **ImportType0**、 **1**、および **2** に適用されます。|Leaf<br /><br /> [統合]|  
|210006|メンバー コードが非アクティブです。|**Importtype**  = **1** で、存在しないメンバーコードを指定しました。|Leaf<br /><br /> [統合]<br /><br /> Relationship|  
|210032|階層名が指定されていないか、無効です。|明示的階層が見つからなかったか、 **HierarchyName** の値が空白でした。|[統合]<br /><br /> Relationship|  
|210035|コード生成のビジネス ルールが存在しないので、 **MemberCode** は必須です。|メンバーを作成または更新するとき、自動コード生成を使用しない場合は、 **MemberCode** が常に必須です。 詳細については、「 [自動コード作成 &#40;マスターデータサービス&#41;](../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。|Leaf<br /><br /> [統合]|  
|210036|コード生成のビジネス ルールが存在するため、 **MemberCode** を指定する必要はありません。|メンバーを作成または更新するとき、自動コード生成を使用している場合は、 **MemberCode** は必要ありません。 ただし、指定してもかまいません。 詳細については、「 [自動コード作成 &#40;マスターデータサービス&#41;](../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。|Leaf<br /><br /> [統合]|  
|210041|"ROOT" は有効なメンバー コードではありません。|**Membercode** の値には "ROOT" という単語が含まれています。|Leaf<br /><br /> [統合]<br /><br /> Relationship|  
|210042|"MDMUNUSED" は有効なメンバー コードではありません。|**Membercode** の値に "MDMUNUSED" という単語が含まれています。|Leaf<br /><br /> [統合]<br /><br /> Relationship|  
|210052|MemberCode は、ドメイン ベースの属性値として使用されているため、非アクティブ化できません。|**Importtype** が  =  **3** または **4** のとき、メンバーが他のメンバーの属性値として使用されている場合、ステージングは失敗します。 **ImportType5** または **6** のいずれかを使用して、値を NULL に設定するか、ステージング プロセスを実行する前に値を変更してください。|Leaf<br /><br /> [統合]|  
|300002|メンバー コードが無効です。|リレーションシップ: 親または子のどちらかのメンバー コードが存在しません。<br /><br /> リーフまたは統合: **importtype**  =  **3** または **4** で、メンバーコードが存在しません。|Leaf<br /><br /> [統合]<br /><br /> Relationship|  
|300004|このメンバー コードは既に存在します。|**Importtype**  = **1** で、エンティティに既に存在するメンバーコードを使用しました。|Leaf<br /><br /> [統合]|  
|210011|**RelationshipType** が **1** の場合、 **ParentCode** はリーフ メンバーにできません。|**ParentCode** の値が統合メンバー コードであることを確認してください。|Relationship|  
|210015|階層およびバッチのステージング テーブルに、メンバー コードが複数回出現します。|明示的階層の場合に、同じバッチ内で同じメンバーの位置を複数回指定しました。|Relationship|  
|210016|循環参照が発生するため、リレーションシップを作成できませんでした。|子を親として割り当てようとした場合に、このエラーが発生します。|Relationship|  
|210046|Root の兄弟をメンバーにすることはできません。|このエラーは、 **RelationshipType**  =  **2** (兄弟) と **parentcode** または **childcode** のどちらかが **Root** の場合に発生します。 メンバーは、ルート ノードと同じレベルに存在することはできません (子しかメンバーになれません)。|Relationship|  
|210047|Unused の兄弟をメンバーにすることはできません。|このエラーは、 **RelationshipType**  =  **2** (兄弟) と **parentcode** または **childcode** のどちらかが使用されてい **ない** 場合に発生します。 未使用ノードの子しかメンバーになれません。|Relationship|  
|210048|**ParentCode** と **ChildCode** を同じにすることはできません。|**ParentCode** の値は **ChildCode** の値と同じです。 これらの値は別にする必要があります。|Relationship|  
  
## <a name="see-also"></a>参照  
 [ステージング &#40;マスターデータサービス中に発生したエラーを表示&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [概要: テーブルからデータをインポートする (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
