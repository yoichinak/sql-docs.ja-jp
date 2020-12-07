---
description: 予約語 (マスター データ サービス)
title: 予約語
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5eff7f5f2db1d1b155b94818083ddad11f23890e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456716"
---
# <a name="reserved-words-master-data-services"></a>予約語 (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、モデル オブジェクトまたはメンバーを作成するときに使用できない単語がいくつかあります。 これらの単語を使用すると、エラーが発生する可能性があります。  
  
> [!NOTE]  
>  特殊文字 (記号、ハイフネーションなど) の使用も極力控えてください。  
  
-   [Models](../master-data-services/reserved-words-master-data-services.md#models)  
  
-   [エンティティ](../master-data-services/reserved-words-master-data-services.md#entities)  
  
-   [明示的階層](../master-data-services/reserved-words-master-data-services.md#exhierarchies)  
  
-   [属性](../master-data-services/reserved-words-master-data-services.md#attributes)  
  
-   [[メンバー]](../master-data-services/reserved-words-master-data-services.md#members)  
  
##  <a name="models"></a><a name="models"></a> モジュール  
 名前を **Name** または **Code**に設定したモデルを作成する場合は、 **[モデルと同じ名前のエンティティを作成する]** を選択しないでください。エンティティの名前に **Name** または **Code** は使用できません。  
  
##  <a name="entities"></a><a name="entities"></a> 事業  
 エンティティ名には **Name** または **Code**を使用できません。  
  
##  <a name="explicit-hierarchies"></a><a name="exhierarchies"></a> 明示的階層  
 明示的階層名には **Name** または **Code**を使用できません。  
  
##  <a name="attributes"></a><a name="attributes"></a> アトリビュート  
  
-   **ID**  
  
-   **コード**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
-   **名前**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a><a name="members"></a> 属する  
 メンバーの場合、 **MDMMemberStatus**、 **MDMUnused**、または **ROOT** を **Code** 属性値として使用することはできません。  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスの概要 (MDS)](../master-data-services/master-data-services-overview-mds.md)  
  
  
