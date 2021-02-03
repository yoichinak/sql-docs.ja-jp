---
description: MSSQLSERVER_12301
title: MSSQLSERVER_12301 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 12301 (Database Engine error)
ms.assetid: 69455df4-4ce9-4a6f-af5a-8bbc93e21245
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 53595bd38760418dbd550995126a90eae58d9860
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197134"
---
# <a name="mssqlserver_12301"></a>MSSQLSERVER_12301
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|12301|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|HK_UNSUPPORTED_NULLABLE_COLUMNS|  
|メッセージ テキスト|インデックス キー内の NULL 値を許容する列は '*construct*' でサポートされていません。|  
  
## <a name="user-action"></a>ユーザーの操作  
インデックス キー内では NULL 値を許容する列を使用しないでください。  
  
## <a name="see-also"></a>参照  
[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
