---
description: '[ターゲット サーバー] ([ターゲット サーバーの状態] タブ)'
title: '[ターゲット サーバー] ([ターゲット サーバーの状態] タブ)'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.target.status.f1
ms.assetid: 010a4cab-d878-4889-8ac8-7d91db6345d6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9d296f5c98466bfd8981053f571a6a3212091d8a
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037769"
---
# <a name="target-servers-target-server-status-tab"></a>[ターゲット サーバー] ([ターゲット サーバーの状態] タブ)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このページを使用すると、このマスター サーバーのターゲット サーバーの状態を表示できます。  
  
## <a name="options"></a>オプション  
**[ターゲット サーバー]**  
ターゲット サーバーの名前を表示します。  
  
**[ローカル時刻]**  
ターゲット サーバーのローカル タイム ゾーンにおける日付と時刻を表示します。  
  
**[最終呼び出し]**  
ターゲット サーバーがマスターの呼び出しを行った最新の日時を、そのサーバーのローカル時刻で表示します。  
  
**[未読の命令]**  
ターゲット サーバーが受け取っていない命令の数を表示します。  
  
**状態**  
ターゲット サーバーの状態を表示します。  
  
**[強制的にポーリング]**  
このボタンをクリックすると、選択されているターゲット サーバーがマスター サーバーをポーリングします。  
  
**[強制的に参加解除]**  
このボタンをクリックすると、選択されているターゲット サーバーがマスター サーバーを登録解除します。  
  
**[命令を通知]**  
選択されているターゲット サーバーに命令を通知します。  
  
**[自動更新を有効にする]**  
このオプションをオンにすると、表示されている情報が自動的に更新されます。  
  
**[更新間隔]**  
このページの情報を更新する間隔を指定します。  
  
## <a name="see-also"></a>参照  
[エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
