---
description: MSSQLSERVER_12304
title: MSSQLSERVER_12304 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 484046de79a34997f4e0c77cc0ff56f9c2c2452c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197098"
---
# <a name="mssqlserver_12304"></a>MSSQLSERVER_12304
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|12304|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|メッセージ テキスト|ネイティブ コンパイル ストアド プロシージャのコンテキスト外にある型を使用する場合は、自らの任意の列と共に IDENTITY プロパティを使用するメモリ最適化テーブルを使用することはサポートされていません。|  
  
## <a name="user-action"></a>ユーザーの操作  
自らの任意の列と共に IDENTITY プロパティを使用するメモリ最適化テーブル型を使用しないでください。  
  
## <a name="see-also"></a>参照  
[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
