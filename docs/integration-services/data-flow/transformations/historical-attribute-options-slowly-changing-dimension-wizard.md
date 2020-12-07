---
description: '[履歴属性オプション] (緩やかに変化するディメンション ウィザード)'
title: 履歴属性オプション (緩やかに変化するディメンション ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9610a734543c9199e54d3f8489d86e03089f10ed
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88430704"
---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>[履歴属性オプション] (緩やかに変化するディメンション ウィザード)

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  **[履歴属性オプション]** ダイアログ ボックスを使用すると、開始日や終了日によって履歴属性を表示したり、専用に作成された列に履歴属性を記録したりできます。  
  
 このウィザードの詳細については、「 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)」を参照してください。  
  
## <a name="options"></a>Options  
 **[現在のレコードと有効期限が切れたレコードを 1 列で表示する]**  
 1 列を使用して履歴属性のステータスを記録する場合は、次のオプションを使用できます。  
  
|オプション|説明|  
|------------|-----------------|  
|**[現在のレコードを示す列]**|現在のレコードを示す列を選択します。|  
|**[現時点での値]**|**[True]** または **[Current]** を使用してレコードが現在のレコードであるかどうかを示します。|  
|**[有効期限切れの値]**|**[False]** または **[Expired]** を使用してレコードが履歴の値であるかどうかを示します。|  
  
 **[開始日と終了日を使用して現在のレコードと有効期限が切れたレコードを識別する]**  
 このオプションのディメンション テーブルには、日付列を含める必要があります。 履歴属性を開始日および終了日を使用して示す場合は、次のオプションを使用できます。  
  
|オプション|説明|  
|------------|-----------------|  
|**[開始日の列]**|ディメンション テーブルで開始日を含む列を選択します。|  
|**[終了日の列]**|ディメンション テーブルで終了日を含む列を選択します。|  
|**[日付の値を設定する変数]**|日付の変数を一覧から選択します。|  
  
## <a name="see-also"></a>参照  
 [緩やかに変化するディメンション ウィザードを使用して出力を構成する](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
