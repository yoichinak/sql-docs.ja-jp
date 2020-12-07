---
description: MSSQLSERVER_845
title: MSSQLSERVER_845 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b4d474714579397d18e22f2c32cc540ff30d5ac0
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618078"
---
# <a name="mssqlserver_845"></a>MSSQLSERVER_845
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|845|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|BUFLATCH_TIMEOUT|  
|メッセージ テキスト|バッファー ラッチを待機中にタイムアウトが発生しました。ページ %S_PGID の型 %d、データベース ID %d。|  
  
## <a name="explanation"></a>説明  
ラッチを取得するためにプロセスが待機中でしたが、制限時間に達したため、取得できませんでした。 このエラーは、I/O 操作の完了までに時間がかかりすぎる場合に発生する可能性があります。通常は、他のタスクによってシステムのプロセスが中断された結果のエラーです。 場合によっては、ハードウェア障害によってこのエラーが生じることもあります。  
  
## <a name="cause"></a>原因
このエラー メッセージは、ご利用のシステムの全体的な環境によって異なります。 次のような環境では、システムの負荷が過剰になる可能性があります。

- 入出力 (I/O) とメモリのニーズを満たしていないハードウェア
- 不適切に構成およびテストされた設定
- 非効率的な設計

 システムの負荷が高く、ワークロードの要求を満たせない場合、エラー 845 が発生することがあります。 負荷の高い環境の一般的な原因には、次のようなものがあります。

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
- 845 エラー メッセージが頻繁に発生しない場合は、エラーを無視してかまいません