---
description: EditModeEnum
title: EditModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c8aafe9069f1ea6718713ddb2239e4e9699ee48
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167503"
---
# <a name="editmodeenum"></a>EditModeEnum
レコードの編集状態を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|編集操作が実行中でないことを示します。|  
|**adEditInProgress**|1|現在のレコードのデータが変更されていても保存されていないことを示します。|  
|**adEditAdd**|2|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)メソッドが呼び出され、コピーバッファー内の現在のレコードが、データベースに保存されていない新しいレコードであることを示します。|  
|**adEditDelete**|4|現在のレコードが削除されたことを示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
  
## <a name="applies-to"></a>適用対象  
 [EditMode プロパティ](../../../ado/reference/ado-api/editmode-property.md)
