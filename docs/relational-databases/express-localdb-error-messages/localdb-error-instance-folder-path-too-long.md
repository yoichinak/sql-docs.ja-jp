---
description: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: a4313aa27b2bae30f6eb989e2161b80635a2b985
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506226"
---
# <a name="localdb_error_instance_folder_path_too_long"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>詳細  
  
| 属性 | 値 |
| --------- | ----- | 
|製品名|SQL Server|  
|イベント ID|260|  
|イベント ソース|SQL Server Local Database Runtime 12.0|  
|コンポーネント|Local Database Runtime API|  
|メッセージ テキスト|ローカル データベース インスタンス フォルダーの完全なパスの長さが MAX_PATH よりも長くなっています。 インスタンスは、次のフォルダーに格納されている必要があります:%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server ローカル Db\ インスタンス \\<インスタンス名 \> 。|  
  
## <a name="explanation"></a>説明  
 インスタンスを格納するパスの長さが MAX_PATH を超過しています。  
  
## <a name="user-action"></a>ユーザーの操作  
 MAX_PATH よりも短い新しいパスを作成してください。  
  
  
