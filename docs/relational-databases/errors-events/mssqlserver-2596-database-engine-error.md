---
description: MSSQLSERVER_2596
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce3ed3f225671a762ba6e39f958c6347f813076f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88410858"
---
# <a name="mssqlserver_2596"></a>MSSQLSERVER_2596
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|2596|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|メッセージ テキスト|修復ステートメントは処理されませんでした。 データベースを読み取り専用モードにすることはできません。|  
  
## <a name="explanation"></a>説明  
このメッセージは、データベースが読み取り専用モードであることを示しています。 データベースが読み取り専用モードである場合は、修復が不可能です。  
  
## <a name="user-action"></a>ユーザーの操作  
ALTER DATABASE を使用してデータベースを読み取り/書き込み可能に設定し、DBCC コマンドを再実行します。  
  
## <a name="see-also"></a>参照  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  
