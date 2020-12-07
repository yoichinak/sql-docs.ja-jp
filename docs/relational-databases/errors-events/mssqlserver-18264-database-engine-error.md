---
description: MSSQLSERVER_18264
title: MSSQLSERVER_18264 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18264 (Database Engine error)
ms.assetid: 3050fc56-2be5-43cf-916b-50a3ac5f89aa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ce3007856d44fa513c7397cc37af880f6a21c5a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385754"
---
# <a name="mssqlserver_18264"></a>MSSQLSERVER_18264
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|Microsoft SQL Server|  
|イベント ID|18264|  
|イベント ソース|MSSQLENGINE|  
|コンポーネント|SQLEngine|  
|シンボル名|STRMIO_DBDUMP|  
|メッセージ テキスト|データベースがバックアップされました。 データベース: %s、作成日 (時間): %s(%s)、ダンプされたページ: %d、最初の LSN: %s、最後の LSN: %s、ダンプ デバイスの数: %d、デバイス情報: (%s)。 このメッセージは情報提供だけを目的としています。 ユーザーによる操作は不要です。|  
  
## <a name="explanation"></a>説明  
既定では、バックアップが成功するたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにこの情報メッセージが追加されます。 トランザクション ログを頻繁にバックアップすると、これらのメッセージがすぐに蓄積され、他のメッセージを探すのが困難になるほど大きなエラー ログが生成されることがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のトレース フラグ **3226** を使用すると、これらのログ エントリを除外できます。 頻度の高いログ バックアップを実行している場合やスクリプトがこれらのエントリに依存していない場合は、このトレース フラグを有効にすると便利です。  
  
トレース フラグの使用方法の詳細については、SQL Server オンライン ブックを参照してください。  
  
## <a name="see-also"></a>参照  
[トレース フラグ &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
