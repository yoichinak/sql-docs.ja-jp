---
description: MSSQLSERVER_17083
title: MSSQLSERVER_17083 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 17083 (Database Engine error)
ms.assetid: 6c83737d-0531-4fd9-88f6-2da5a150532d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0ad348d202855fa1237d288b81880f4f342c2009
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196813"
---
# <a name="mssqlserver_17083"></a>MSSQLSERVER_17083
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|17083|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|P3_HEKATON_NOT_ATOMIC|  
|メッセージ テキスト|ネイティブ コンパイル ストアド プロシージャの本体は ATOMIC ブロックである必要があります。|  
  
## <a name="explanation"></a>説明  
ネイティブ コンパイル ストアド プロシージャの本体に ATOMIC ブロックがありませんでした。  
  
## <a name="user-action"></a>ユーザーの操作  
ネイティブ コンパイル ストアド プロシージャには ATOMIC ブロックが必要です。 次に例を示します。  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
