---
description: MSSQLSERVER_1203
title: MSSQLSERVER_1203 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1203 (Database Engine error)
ms.assetid: 33a35f00-98c8-46c6-b432-544b326b6117
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d430fa9aad8314e134a5b8de37d09a121b499dbe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88336338"
---
# <a name="mssqlserver_1203"></a>MSSQLSERVER_1203
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|1203|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LK_NOT|  
|メッセージ テキスト|プロセス ID %d は、所有していないリソース %.*ls のロックを解除しようとしました。 このエラーはタイミングによって発生する可能性があるので、トランザクションを再試行してください。 問題が解決しない場合は、データベース管理者に問い合わせてください。|  
  
## <a name="explanation"></a>説明  
このエラーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が通常の後処理以外の何らかの処理を実行中に、ロックの解除を試みた特定のページのロックが既に解除されていることを検出した場合に発生します。  
  
### <a name="possible-causes"></a>考えられる原因  
このエラーの根本原因は、影響を受けたデータベース内の構造上の問題に関連している可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、マルチユーザー環境でのコンカレンシー制御を管理するために、ページの取得と解放を管理します。 このメカニズムは、存在するロックのページと種類を識別するさまざまな内部ロック構造を使用することにより管理されます。 影響するページを処理するためにロックを取得し、処理が終了すると解放します。  
  
## <a name="user-action"></a>ユーザーの操作  
オブジェクトが所属するデータベースに対して DBCC CHECKDB を実行します。 DBCC CHECKDB でエラーが報告されない場合、接続を再度確立してコマンドを実行します。  
  
> [!IMPORTANT]  
> いずれかの REPAIR 句を指定して DBCC CHECKDB を実行してもこの問題が解決しない場合、または REPAIR 句を指定して DBCC CHECKDB を実行した場合のデータへの影響がわからない場合は、購入元にお問い合わせください。  
  
