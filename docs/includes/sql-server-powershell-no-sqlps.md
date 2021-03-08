---
title: PowerShell での SQL Server エージェントに対する NOSQLPS の使用
description: SQL Server エージェントで PowerShell の sqlps コマンドレットではなく sqlserver コマンドレットを使用するように説明するメッセージ
ms.topic: include
author: markingmyname
ms.author: maghan
ms.reviewer: drskwier
ms.openlocfilehash: bf161bd583f3d48dc389cea6b69f55c32e2cce59
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101839408"
---
SQL Server 2019 以降では、SQLPS を無効にすることができます。 PowerShell 型のジョブ ステップの最初の行に `#NOSQLPS` を追加します。これにより、SQL Agent による SQLPS モジュールの自動読み込みは停止されます。 これにより、コンピューターにインストールされている PowerShell のバージョンが、SQL Agent ジョブによって実行されるようになり、希望する他の任意の PowerShell モジュールを使用できます。

SQL Agent ジョブ ステップで [**SqlServer モジュール**](https://www.powershellgallery.com/packages/Sqlserver/21.1.18235)を使用するには、次のコードをスクリプトの最初の 2 行にします。

```powershell
#NOSQLPS
Import-Module -Name SqlServer
```