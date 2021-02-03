---
description: MSSQLSERVER_15517
title: MSSQLSERVER_15517 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 592439f0e90f1b8ba607f518ad5125510b8e8a3e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196897"
---
# <a name="mssqlserver_15517"></a>MSSQLSERVER_15517
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|15517|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SEC_CANNOTEXECUTEASUSER|  
|メッセージ テキスト|データベース プリンシパルとして実行できません。プリンシパル "*principal*" が存在しないか、この種類のプリンシパルで権限を借用できないか、ユーザーに権限がありません。|  
  
## <a name="user-action"></a>ユーザーの操作  
既存のプリンシパルの名前を使用するか、そのプリンシパルに対する IMPERSONATE 権限を取得します。  
  
15517 は、元のデータベースの所有者以外のユーザーによってデータベースのアタッチおよび復元が実行された後に発生する可能性があります。 このエラーを解決するには、次のコマンドを実行して、サーバーにログインするための db_owner を変更します。  
  
```  
ALTER AUTHORIZATION ON DATABASE:: DBName TO [NewLogin]  
```  
  
## <a name="see-also"></a>参照  
[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
