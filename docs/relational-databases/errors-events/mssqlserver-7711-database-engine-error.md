---
description: MSSQLSERVER_7711
title: MSSQLSERVER_7711 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7711 (Database Engine error)
ms.assetid: a5c7cd6e-18d6-47ef-902b-db9dd64bba34
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7b31daec8051ea8bd4a4ea8a73d6754e2014edbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460929"
---
# <a name="mssqlserver_7711"></a>MSSQLSERVER_7711
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|7711|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PRT_RANGE_OVERLAP|  
|メッセージ テキスト|テーブル、インデックス、またはパーティションの 1 つに DATA_COMPRESSION オプションが複数回指定されました。|  
  
## <a name="explanation"></a>説明  
次のステートメントのいずれかの DATA_COMPRESSION オプションでエラーが発生しました。  
  
-   CREATE TABLE  
  
-   ALTER TABLE  
  
-   CREATE INDEX  
  
-   ALTER INDEX  
  
引用されたテーブルまたはインデックスがパーティション分割されている場合、少なくとも 1 つのパーティションで DATA_COMPRESSION オプションが 2 回以上指定されました。 テーブルまたはインデックスがパーティション分割されていない場合、DATA_COMPRESSION オプションが 2 回以上引用されました。  
  
## <a name="user-action"></a>ユーザーの操作  
パーティション分割されたテーブルまたはインデックスの場合、各パーティションに DATA_COMPRESSION オプションを 1 回だけ指定するようにしてください。 パーティション分割されていないテーブルまたはインデックスの場合、ステートメントに DATA_COMPRESSION オプションを 1 回だけ使用してください。  
  
