---
description: MSSQLSERVER_3417
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c8a7cedd7aec428c7b72d07090356977f385e300
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456206"
---
# <a name="mssqlserver_3417"></a>MSSQLSERVER_3417
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|3417|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|REC_BADMASTER|  
|メッセージ テキスト|master データベースを復旧できません。 SQL Server を実行できません。 master データベースを、完全バックアップを使用して復元するか、修復または再構築してください。 master データベースを再構築する方法の詳細については、SQL Server オンライン ブックを参照してください。|  
  
## <a name="explanation"></a>説明  
SQL Server は **master** データベースを起動できません。 **master** または **tempdb** がオンライン状態にならないと、SQL Server は稼働しません。 このエラーは通常、別のエラーの後に発生します。 エラー ログで、根本的な原因を確認してください。  
  
## <a name="user-action"></a>ユーザーの操作  
データベースのバックアップを復元するか、データベースを修復します。  
  
