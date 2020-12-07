---
description: MSSQLSERVER_2546
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d955e5e7a0ab7ec1bc8c34306bc983683275f05c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482817"
---
# <a name="mssqlserver_2546"></a>MSSQLSERVER_2546
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|2546|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_INDEX_MARKED_DISABLED|  
|メッセージ テキスト|テーブル 'OBJECT_NAME' のインデックス 'INDEX_NAME' は無効に設定されています。 オンラインにするには、インデックスを再構築してください。|  
  
## <a name="explanation"></a>説明  
指定されているインデックスは、オフラインまたは無効に設定されています。 そのため、このインデックスをチェックできません。  
  
## <a name="user-action"></a>ユーザーの操作  
ALTER INDEX を使用してインデックスを再構築します。  
  
## <a name="see-also"></a>参照  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[インデックスの再編成と再構築](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
