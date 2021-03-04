---
title: cancel オプション管理ツール
titleSuffix: SQL Server Distributed Replay
description: この記事では、SQL Server 分散再生管理ツールの cancel コマンドライン オプションと構文について説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 21d1d74439b41a6e36287fef957c6c2df24aa1c1
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101836929"
---
# <a name="cancel-option-distributed-replay-administration-tool"></a>cancel オプション (Distributed Replay 管理ツール)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生管理ツールである **DReplay.exe** は、分散再生コントローラーと通信するために使用できるコマンド ライン ツールです。 このトピックでは、 **cancel** コマンド ライン オプションとそれに対応する構文について説明します。  
  
 **cancel** オプションは、コントローラーで実行されている現在の操作をキャンセルします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") 管理ツールの構文で使用される構文表記規則の詳細については、「[Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
dreplay cancel [-m controller] [-q]   
```  
  
#### <a name="parameters"></a>パラメーター
 **-m** *controller*  
 コントローラーのコンピューター名です。 "`localhost`" または "`.`" を使用してローカル コンピューターを参照できます。  
  
 **-m** パラメーターが指定されていない場合、ローカル コンピューターが使用されます。  
  
 **-q**  
 非表示モードです。 確認のプロンプトは表示されません。  
  
 **-q** パラメーターは省略可能です。  
  
## <a name="examples"></a>例  
 次の例では、非表示モードでキャンセル要求が送信されます。 値 `localhost` は、コントローラー サービスが管理ツールと同じコンピューターで実行されていることを示します。  
  
```  
dreplay cancel -m localhost -q  
```  
  
## <a name="permissions"></a>アクセス許可  
 対話ユーザー (ローカル ユーザーまたはドメイン ユーザー アカウント) として、管理ツールを実行する必要があります。 ローカル ユーザー アカウントを使用するには、管理ツールとコントローラーが同じコンピューター上で実行されている必要があります。  
  
 詳細については、「 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
