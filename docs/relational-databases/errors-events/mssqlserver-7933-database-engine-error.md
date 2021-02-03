---
description: MSSQLSERVER_7933
title: MSSQLSERVER_7933 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 7933 (Database Engine error)
ms.assetid: 722bd2c6-0fb9-4838-954a-439744c6ac4b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0a9ec7e3c03206136ec3883e1e15ab4d4443d2b7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197989"
---
# <a name="mssqlserver_7933"></a>MSSQLSERVER_7933
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|7933|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC2_FS_ORPHANED_ROWSET_DIRECTORY|  
|メッセージ テキスト|テーブル エラー:パーティションの FileStream ディレクトリ ID F_ID は存在しますが、対応するパーティションがデータベース内に存在しません。|  
  
## <a name="explanation"></a>説明  
DBCC CHECKDB の実行中に、FILESTREAM データ領域で行セット ディレクトリが見つかりましたが、対応するパーティションがデータベース内にありません。  
  
## <a name="user-action"></a>ユーザーの操作  
  
### <a name="look-for-hardware-failure"></a>ハードウェア障害を調査する  
ハードウェアの診断を実行し、問題があれば修正します。 また、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のシステム ログとアプリケーション ログ、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログを調査し、ハードウェア障害の結果としてエラーが発生しているかどうかを確認します。 ログに記録されているハードウェアに関する問題があれば、それを修正します。  
  
データ破損の問題が解決しない場合は、ハードウェア コンポーネントを他のものと交換し、問題の原因を特定するようにしてください。 システムで、ディスク コントローラーの書き込みキャッシュが有効になっていないことを確認します。 書き込みキャッシュが問題と思われる場合は、ハードウェア ベンダーにお問い合わせください。  
  
それでも問題が解決しない場合は、新しいハードウェア システムの導入をご検討ください。 導入の際には、ディスク ドライブの再フォーマットとオペレーティング システムの再インストールが必要になる場合があります。  
  
### <a name="restore-from-backup"></a>バックアップから復元する  
問題がハードウェアに関するものではなく、また既知のクリーン バックアップがある場合は、そのバックアップを使用してデータベースを復元します。  
  
### <a name="run-dbcc-checkdb"></a>DBCC CHECKDB の実行  
適用不可。 このエラーを自動的に修正することはできません。 バックアップからデータベースを復元できない場合は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタマー サポート サービス (CSS) にご連絡ください。  
  
