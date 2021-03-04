---
title: 管理ツール コマンドラインオプション
description: SQL Server 分散再生管理ツールである DReplay.exe は、分散再生コントローラーと通信するためのコマンド ライン ツールです。
titleSuffix: SQL Server Distributed Replay
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/12/2016
ms.openlocfilehash: 80cb7abb5f1bf3511b30719563908f0b59cecc93
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101836949"
---
# <a name="administration-tool-command-line-options-distributed-replay-utility"></a>管理ツール コマンド ライン オプション (Distributed Replay Utility)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理ツールである **DReplay.exe** は、Distributed Replay Controller と通信するためのコマンド ライン ツールです。 管理ツールを使用して、コントローラー上の操作を開始、監視、取り消しできます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") 管理ツールの構文で使用される構文表記規則の詳細については、「[Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
dreplay {preprocess|replay|status|cancel} [options] [-?]}  
  
Usage:  
  
  dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
  
  dreplay replay [-m controller] -d controller_working_dir [-o]  
    [-s target_server] -w clients [-c config_file]  
    [-f status_interval]  
  
  dreplay status [-m controller] [-f status_interval]  
  
  dreplay cancel [-m controller] [-q]   
```  
  
## <a name="remarks"></a>解説  
 **DReplay.exe** では、次のコマンド ライン オプションを発行することができます。  
  
 **preprocess**  
 前処理段階を開始します。 コントローラーは、ターゲット サーバーに対する再生のために、運用環境からキャプチャした入力トレース データの準備を行います。  
  
 **再生 (replay)**  
 イベント再生段階を開始します。 コントローラーは、指定されたクライアントに再生データをディスパッチし、分散再生を開始して、クライアントを同期します。 必要に応じて、選択された各クライアントは、再生アクティビティを記録し、結果トレース ファイルをローカルに保存します。  
  
 **status**  
 コントローラーにクエリし、現在の状態を表示します。  
  
 **cancel**  
 コントローラーで実行されている現在の操作を取り消します。  
  
 コマンドの引数や例などの構文情報の詳細については、次のトピックを参照してください。  
  
-   [前処理オプション &#40;Distributed Replay 管理ツール&#41;](../../tools/distributed-replay/preprocess-option-distributed-replay-administration-tool.md)  
  
-   [replay オプション &#40;Distributed Replay 管理ツール&#41;](../../tools/distributed-replay/replay-option-distributed-replay-administration-tool.md)  
  
-   [status オプション &#40;Distributed Replay 管理ツール&#41;](../../tools/distributed-replay/status-option-distributed-replay-administration-tool.md)  
  
-   [cancel オプション &#40;Distributed Replay 管理ツール&#41;](../../tools/distributed-replay/cancel-option-distributed-replay-administration-tool.md)  
  
 RPC は、言語イベントとしてではなく RPC として再生されます。  
  
## <a name="permissions"></a>アクセス許可  
 対話ユーザー (ローカル ユーザーまたはドメイン ユーザー アカウント) として、管理ツールを実行する必要があります。 ローカル ユーザー アカウントを使用するには、管理ツールとコントローラーが同じコンピューター上で実行されている必要があります。  
  
 詳細については、「 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
