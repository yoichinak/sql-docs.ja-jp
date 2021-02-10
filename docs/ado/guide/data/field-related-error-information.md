---
description: フィールドに関連するエラー情報
title: Field-Related のエラー情報 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
author: rothja
ms.author: jroth
ms.openlocfilehash: cce74cf105aa7b38c2a3d7b157ef0fa17a1e8c1f
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037472"
---
# <a name="field-related-error-information"></a>フィールドに関連するエラー情報
データが欠落している場合や、フィールドの型が正しくない場合などに、エラーがフィールドに直接関連している場合は、 **フィールド** オブジェクトの **Status** プロパティを調べて、問題の原因に関する詳細情報を取得できます。 このプロパティは、問題に関する特定の情報を提供するように強化されています。 そのため、たとえば、 **UpdateBatch** の呼び出しが失敗した場合は、影響を受ける各レコードの **フィールド** の **Status** プロパティを調べて、問題の原因を特定できます。 プロパティは、 **Fieldstatusenum** 定数内のいずれかの値を格納します。 次の表には、エラーが発生した場合に特に関心のある値が含まれています。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|データを失うことなく、フィールドを取得または保存できないことを示します。|  
|**adFieldDataOverflow**|6|プロバイダーから返されたデータがフィールドのデータ型でオーバーフローしたことを示します。|  
|**adFieldDefault**|13|データを設定するときにフィールドの既定値が使用されたことを示します。|  
|**adFieldIgnore**|15|ソースでデータ値を設定するときに、このフィールドがスキップされたことを示します。 プロバイダーによって値が設定されませんでした。|  
|**adFieldIntegrityViolation**|10|計算されたエンティティまたは派生エンティティであるため、フィールドを変更できないことを示します。|  
|**Adの Disnull**|3|プロバイダーが null 値を返したことを示します。|  
|**adFieldOutOfSpace**|22|移動またはコピー操作を完了するのに十分な記憶域スペースをプロバイダーが取得できないことを示します。|
