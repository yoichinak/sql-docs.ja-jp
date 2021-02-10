---
description: SaveOptionsEnum
title: SaveOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: rothja
ms.author: jroth
ms.openlocfilehash: db94b409a799a24d0c74dfec5a3d388c55df20e2
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100040672"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
[ストリーム](./stream-object-ado.md)オブジェクトから保存するときにファイルを作成するか上書きするかを指定します。 値には、 **adSaveCreateNotExist** または **adSaveCreateOverWrite** を指定できます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|既定値。 *FileName* パラメーターで指定したファイルがまだ存在しない場合は、新しいファイルを作成します。|  
|**adSaveCreateOverWrite**|2|*Filename* パラメーターで指定されたファイルが既に存在する場合、ファイルを現在開いている **ストリーム** オブジェクトのデータで上書きします。 *Filename* パラメーターで指定されたファイルが存在しない場合は、新しいファイルが作成されます。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [SaveToFile メソッド](./savetofile-method.md)