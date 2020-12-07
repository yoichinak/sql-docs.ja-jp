---
description: 編集モードの決定
title: 編集モードの決定 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: rothja
ms.author: jroth
ms.openlocfilehash: ec235cfd012b79449fdebfab9c99399d967ca32f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991363"
---
# <a name="determining-edit-mode"></a>編集モードの決定
ADO は、現在のレコードに関連付けられている編集バッファーを保持します。 **EditMode**プロパティは、このバッファーに変更が加えられたかどうか、または新しいレコードが作成されたかどうかを示します。 現在のレコードの編集状態を確認するには、 **EditMode** を使用します。 編集プロセスが中断されている場合は、保留中の変更をテストし、 **Update** または **CancelUpdate** メソッドを使用する必要があるかどうかを判断できます。  
  
 **EditMode** は、次の表に示すいずれかの **editmodeenum** 定数を返します。  
  
|定数|説明|  
|--------------|-----------------|  
|**adEditNone**|編集操作が実行中でないことを示します。|  
|**adEditInProgress**|現在のレコードのデータが変更されていても保存されていないことを示します。|  
|**adEditAdd**|**AddNew**メソッドが呼び出され、コピーバッファー内の現在のレコードが、データベースに保存されていない新しいレコードであることを示します。|  
|**adEditDelete**|現在のレコードが削除されたことを示します。|  
  
 **EditMode** は、現在のレコードがある場合にのみ、有効な値を返すことができます。 **BOF**または**EOF**が**True**の場合、または現在のレコードが削除されている場合、 **EditMode**はエラーを返します。
