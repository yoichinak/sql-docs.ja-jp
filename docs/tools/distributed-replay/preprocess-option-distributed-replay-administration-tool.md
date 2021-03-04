---
title: preprocess オプション
titleSuffix: SQL Server Distributed Replay
description: Microsoft SQL Server 分散再生ツールである DReplay.exe は、分散再生コントローラーと通信するために使用できるコマンドライン ツールです。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 34c4b1432fa9373e4952bb6b11264f5cec6e452a
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101836862"
---
# <a name="preprocess-option-distributed-replay-administration-tool"></a>前処理オプション (Distributed Replay 管理ツール)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生管理ツールである **DReplay.exe** は、分散再生コントローラーと通信するために使用できるコマンド ライン ツールです。 このトピックでは、 **preprocess** コマンド ライン オプションとそれに対応する構文について説明します。  
  
 **preprocess** オプションは、前処理段階を開始します。 この段階では、ターゲット サーバーに対して、コントローラーが入力トレース データの再生の準備を行います。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") 管理ツールの構文で使用される構文表記規則の詳細については、「[Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
```  
  
#### <a name="parameters"></a>パラメーター  
 **-m** _controller_  
 コントローラーのコンピューターの名前を指定します。 "`localhost`" または "`.`" を使用してローカル コンピューターを参照できます。  
  
 **-m** パラメーターが指定されていない場合、ローカル コンピューターが使用されます。  
  
 **-i** _input_trace_file_  
 `D:\Mytrace.trc`などの形式で、コントローラー上の入力トレース ファイルの完全なパスを指定します。 **-i** パラメーターは必須です。  
  
 同じディレクトリにロールオーバー ファイルがある場合は、自動的に読み込まれて使用されます。 ファイルは、ファイル ロールオーバー名前付け規則に準拠する必要があります (例: `Mytrace.trc`、`Mytrace_1.trc`、`Mytrace_2.trc`、`Mytrace_3.trc`、... `Mytrace_n.trc`)。  
  
> [!NOTE]  
>  コントローラーとは別のコンピューターで管理ツールを使用している場合は、このパラメーターにローカル パスを使用できるように、コントローラーに入力トレース ファイルをコピーする必要があります。  
  
 **-d** _controller_working_dir_  
 中間ファイルが格納される、コントローラー上のディレクトリを指定します。 **-d** パラメーターは必須です。  
  
 これには次の要件があります。  
  
-   ディレクトリはコントローラー上に置く必要があります。  
  
-   ドライブ文字で始まる完全なパスを指定する必要があります (たとえば、 `c:\WorkingDir`)。  
  
-   パスはバックスラッシュ "`\`" で終了することはできません。  
  
-   UNC パスはサポートされません。  
  
 **-c** _config_file_  
 前処理構成ファイルのフル パスです。別の場所に保存されている前処理構成ファイルの場所を指定するために使用します。 このパラメーターは UNC パスにするか、または管理ツールを実行するコンピューター上にローカルに置くことができます。  
  
 **-c** パラメーターは、フィルターが必要ない場合または最大アイドル時間を変更しない場合は、必要ありません。  
  
 **-c** パラメーターが指定されない場合は、既定の前処理構成ファイル `DReplay.exe.preprocess.config`が使用されます。  
  
 **-f** _status_interval_  
 ステータス メッセージを表示する頻度 (秒単位) を指定します。  
  
 **-f** を指定しない場合は、既定の間隔は 30 秒です。  
  
## <a name="examples"></a>例  
 この例では、すべての既定の設定で前処理段階が開始されます。 値 `localhost` は、コントローラー サービスが管理ツールと同じコンピューターで実行されていることを示します。 *input_trace_file* パラメーターは、入力トレース データ `c:\mytrace.trc`の場所を指定します。 トレース ファイルのフィルターがないため、 **-c** パラメーターを指定する必要はありません。  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir  
```  
  
 この例では、前処理段階が開始され、変更した前処理構成ファイルが指定されます。 前の例とは異なり、 **-c** パラメーターを使用して、別の場所に格納されている変更された構成ファイルを指定しています。 次に例を示します。  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir -c c:\DReplay.exe.preprocess.config  
```  
  
 変更された前処理構成ファイルでは、分散再生中にシステム セッションを除外するフィルター条件が追加されます。 `<PreprocessModifiers>` 要素を前処理構成ファイル `DReplay.exe.preprocess.config`で変更することで、フィルターが追加されます。  
  
 変更された構成ファイルの例を次に示します。  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
## <a name="permissions"></a>アクセス許可  
 対話ユーザー (ローカル ユーザーまたはドメイン ユーザー アカウント) として、管理ツールを実行する必要があります。 ローカル ユーザー アカウントを使用するには、管理ツールとコントローラーが同じコンピューター上で実行されている必要があります。  
  
 詳細については、「 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [入力トレース データの準備](../../tools/distributed-replay/prepare-the-input-trace-data.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [分散再生の構成](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
