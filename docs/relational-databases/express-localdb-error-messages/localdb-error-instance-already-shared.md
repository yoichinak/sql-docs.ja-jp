---
description: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
title: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 35b4d6fa-ebb9-49d3-aaab-d4e37b6f3760
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 4e4b290daa5dee2fb2a7cc5d3d608b81a7eae438
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506267"
---
# <a name="localdb_error_instance_already_shared"></a>LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>詳細  
  
| 属性 | 値 |
| --------- | ----- |
|製品名|SQL Server|  
|イベント ID|284|  
|イベント ソース|SQL Server Local Database Runtime 12.0|  
|コンポーネント|Local Database Runtime API|  
|メッセージ テキスト|指定したローカル データベース インスタンスは既に共有されています。|  
  
## <a name="explanation"></a>説明  
 指定したローカル データベース インスタンスは既に別の共有名で共有されています。  
  
## <a name="user-action"></a>ユーザーの操作  
 共有インスタンスを別の共有名で再度共有する前に、そのインスタンスの共有を解除してください。  
  
  
