---
description: MSSQLSERVER_17065
title: MSSQLSERVER_17065 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 99135bdde28dfaa1cc6b786c7a5e11221abce96f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88333618"
---
# <a name="mssqlserver_17065"></a>MSSQLSERVER_17065
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|17065|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLASSERT_BOTH|  
|メッセージ テキスト|SQL Server アサーション:ファイル: \<%s>、行 = %d 失敗したアサーション = '%s' %s。 このエラーはタイミングに関係している可能性があります。 ステートメントの再実行後もエラーが解決しない場合は、DBCC CHECKDB を使用してデータベースの構造上の整合性を確認するか、またはサーバーを再起動してインメモリ データ構造体が壊れていないことを確認してください。|  
  
## <a name="explanation"></a>説明  
このエラーは、一時的なタイミングに関係する問題や、メモリ内またはディスク上のデータの破損によって発生する可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
例外を発生させたステートメントを再実行します。 タイミングに関係しているイベントによって発生したエラーの場合、エラーは再び発生しません。 問題が引き続き発生する場合は、DBCC CHECKDB を実行してディスク上の破損を確認します。 サーバーを再起動し、インメモリ データ構造体が壊れていないことを確認します。  
  
## <a name="see-also"></a>参照  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
