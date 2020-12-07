---
description: MSSQLSERVER_844
title: MSSQLSERVER_844 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1924a8cc064b9c0c7539802b99013ad28d97ce2a
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618084"
---
# <a name="mssqlserver_844"></a>MSSQLSERVER_844
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|844|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|BUFLATCH_TIMEOUT_CONTINUE|  
|メッセージ テキスト|バッファー ラッチを待機中にタイムアウトが発生しました。型 %d、BP %p、ページ %d:%d、状態 %#x、データベース ID: %d、アロケーション ユニット ID: %I64d%ls、タスク 0x%p : %d、待機時間 %d、フラグ 0x%I64x、所有しているタスク 0x%p。  待機を続行します。|  
  
## <a name="explanation"></a>説明
SQL プロセスが、ラッチの獲得を待機しています。 この問題は、I/O 操作の完了までに時間がかかりすぎている場合に生じることがあります。 このタイプのエラーは、他のタスクによってシステム プロセスがブロックされた結果に生じることが普通です。 場合によっては、ハードウェア障害が原因でこのエラーが生じることもあります。  このエラー メッセージが表示された場合、コンピューターと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が応答を停止している可能性があります。

## <a name="cause"></a>原因
このエラー メッセージは、ご利用のシステムの全体的な環境によって異なります。 次のような環境では、システムの負荷が過剰になる可能性があります。

- 入出力 (I/O) とメモリのニーズを満たしていないハードウェア
- 不適切に構成およびテストされた設定
- 非効率的な設計

 システムの負荷が高く、ワークロードの要求を満たせない場合、エラー 844 が発生することがあります。 負荷の高い環境の一般的な原因には、次のようなものがあります。

- ハードウェアの問題
- 圧縮されたボリューム
- 既定以外の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の構成
- 非効率的なクエリまたはインデックスの設計
- 頻繁なデータベースの AutoGrow または AutoShrink 操作

## <a name="user-action"></a>ユーザーの操作  
このエラーを回避するには、次の操作を試してみます。  
  
- ハードウェアにボトルネックがあるかどうかを判断します。 開始するには、「[ボトルネックの特定](../performance/identify-bottlenecks.md)」を参照してください。 必要に応じて、ご利用の環境の構成、クエリ、負荷のニーズに合わせてハードウェアをアップグレードしてください。

- すべてのハードウェアが正しく機能していることを確認します。 記録されたエラーを確認し、ハードウェア ベンダーの提供する診断を実行します。 エラー ログまたはイベント ログで、関連する I/O エラーがないか調べます。 通常、I/O エラーはディスクに障害があることを示しています。  
- ディスク ボリュームが圧縮されていないことを確認します。 データおよびログ ファイルを圧縮ドライブに格納することはできません。「[データベース ファイルとファイル グループ](../databases/database-files-and-filegroups.md)」を参照してください。 圧縮されたドライブのサポートについては、次の記事を参照してください: 「[圧縮されたボリュームでサポートされていない SQL Server データベース](https://support.microsoft.com/EN-US/help/231347)」。

- 次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成オプションをすべてオフにするとエラーメッセージが消えるかどうかを確認します。
   - [priority boost オプション](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)
   - [lightweight pooling (ファイバー モード) オプション](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)
   - [set working set size オプション](../../database-engine/configure-windows/set-working-set-size-server-configuration-option.md)

    詳細については、「[SQL Server の適切な環境設定を確認する方法](https://support.microsoft.com/EN-US/help/319942)」を参照してください。

- クエリをチューニングして、システムで使用するリソースを削減します。 パフォーマンス チューニングは、システム負荷の削減と、個々のクエリの応答時間改善に役立ちます
- AutoShrink プロパティをオフにして、データベース サイズに対する変更のオーバーヘッドを軽減します
- AutoGrow プロパティに、頻繁になりすぎないように十分な大きさを持った増分値を設定するようにします。 データベース内で使用可能な領域を確認するジョブをスケジュールし、ピーク時以外にデータベース サイズを大きくします。
- 応答していないタスクや他の重大なエラーがないか、エラー ログで調べます。 根底にある問題の根本原因を示している場合があるため、これらのエラーを先に解決してください。
- アサートなどの重大なエラーが頻繁に発生する場合は、その問題を解決します
- 844 エラー メッセージが頻繁に発生しない場合は、エラーを無視してかまいません