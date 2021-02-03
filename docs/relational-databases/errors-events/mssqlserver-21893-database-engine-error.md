---
description: MSSQLSERVER_21893
title: MSSQLSERVER_21893 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d6c77bc40541245f5a713a4548464c377e6d1884
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196358"
---
# <a name="mssqlserver_21893"></a>MSSQLSERVER_21893
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|21893|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum21893|  
|メッセージ テキスト|元のパブリッシャー '%s' のサブスクライバー (%s) は、リダイレクトされたパブリッシャー '%s' でリモート サーバーとして表示されていません。 リダイレクトされたパブリッシャーで **sp_addlinkedserver** を実行して、これらのサブスクライバーをリモート サーバーとして追加してください。|  
  
## <a name="explanation"></a>説明  
**sp_validate_redirected_publisher** は、リモート サーバーでパブリッシャー データベースのサブスクリプション メタデータ テーブルを使用して関連付けられているサブスクライバーを特定し、サブスクライバーの master.dbo.sysservers に関連付けられているエントリがあることを確認します。 このエラーは、特定されたサブスクライバーのいずれかが存在しない場合に発生します。  
  
このエラーは重大なエラーとは見なされません。 新しいパブリッシャーで適切なサブスクライバー エントリを取得できなくてもレプリケーションに対する影響は限定的なため、このエラーが発生するとエージェントは情報としてエラーをログに記録しますが、終了することはありません。 sysservers にサブスクライバーの適切なエントリがないと、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を介して一部のサブスクリプション管理操作を実行したときに失敗する場合があります。 ただし、これらと同じ操作は、管理ストアド プロシージャを明示的に実行することによって正常に実行できます。  
  
## <a name="user-action"></a>ユーザーの操作  
特定されたサブスクライバーのそれぞれについてリダイレクトされたパブリッシャーで **sp_addlinkedserver** を実行し、これらをリモート サーバーとして追加します。 次に、**sp_serveroption** を実行し、サーバーにサブスクライバー ビットを設定します。  
  
