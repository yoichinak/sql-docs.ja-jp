---
description: MSSQLSERVER_945
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2bd18aad57eed6596ff83fc5fddbb50d33cba49a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420896"
---
# <a name="mssqlserver_945"></a>MSSQLSERVER_945
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|945|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DB_IS_SHUTDOWN|  
|メッセージ テキスト|ファイルにアクセスできないか、メモリまたはディスク領域が不足しているので、データベース '%.*ls' を開けません。  詳細については、SQL Server エラー ログを確認してください。|  
  
## <a name="explanation"></a>説明  
ファイルなどのリソースが存在しないため、データベースにアクセスできませんでした。  
  
## <a name="user-action"></a>ユーザーの操作  
エラー ログを参照し、メモリ、ディスク領域、または権限のエラーに関する追加情報を確認してください。 影響を受けたデータベースの .mdf ファイルと .ndf ファイルの場所を確認し、[!INCLUDE[ssDE](../../includes/ssde-md.md)]で使用するアカウントにこれらのファイルへのアクセス権が与えられていることを確認します。 問題を解決した後、データベースを再起動します。この操作を行うには、ALTER DATABASE を使用して、データベースを ONLINE に設定します。  
  
