---
description: SaveOptionsEnum
title: SaveOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: rothja
ms.author: jroth
ms.openlocfilehash: 56e16ff6ca93dde78531394dc474a2e5cc817348
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989313"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
[ストリーム](./stream-object-ado.md)オブジェクトから保存するときにファイルを作成するか上書きするかを指定します。 値には、 **adSaveCreateNotExist** または **adSaveCreateOverWrite**を指定できます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|既定値。 *FileName*パラメーターで指定したファイルがまだ存在しない場合は、新しいファイルを作成します。|  
|**adSaveCreateOverWrite**|2|*Filename*パラメーターで指定されたファイルが既に存在する場合、ファイルを現在開いている**ストリーム**オブジェクトのデータで上書きします。 *Filename*パラメーターで指定されたファイルが存在しない場合は、新しいファイルが作成されます。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [SaveToFile メソッド](./savetofile-method.md)