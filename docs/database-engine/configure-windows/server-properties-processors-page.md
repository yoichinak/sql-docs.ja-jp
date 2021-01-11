---
title: '[サーバーのプロパティ] ([プロセッサ] ページ)'
description: SQL Server のプロセッサの設定について説明します。 ワーカー スレッドの数、プロセッサの割り当て、その他のプロパティを制御するためのオプションについて説明します。
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
author: markingmyname
ms.author: maghan
ms.reviewer: drskwier, matteot
ms.custom: ''
ms.date: 12/17/2020
ms.openlocfilehash: 874cbbae2b418e9b9e06c7a95d62d34a99af38f5
ms.sourcegitcommit: a81823f20262227454c0b5ce9c8ac607aaf537e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/18/2020
ms.locfileid: "97684211"
---
# <a name="server-properties-processors-page"></a>[サーバーのプロパティ] ([プロセッサ] ページ)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

このページを使用すると、プロセッサ オプションを表示または変更できます。 プロセッサの関係の設定は、複数のプロセッサが実装されている場合のみ有効です。  

## <a name="options"></a>Options

### <a name="processor-affinity"></a>[プロセッサの関係]
プロセッサの再読み込みを防ぎ、プロセッサ間のスレッドの移行を少なくするために、プロセッサを特定のスレッドに割り当てます。 詳細については、「 [affinity mask サーバー構成オプション](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)」を参照してください。

### <a name="io-affinity"></a>[I/O 関係]
[!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server ディスク I/O を特定の CPU のサブセットにバインドします。 詳細については、「 [affinity Input-Output mask サーバー構成オプション](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)」を参照してください。

### <a name="automatically-set-processor-affinity-mask-for-all-processors"></a>[すべてのプロセッサに対して自動的にプロセッサ関係マスクを設定する]
プロセッサの関係が SQL Server によって設定されます。

### <a name="automatically-set-io-affinity-mask-for-all-processors"></a>[すべてのプロセッサに対して自動的に I/O 関係マスクを設定する]
I/O 関係が SQL Server によって設定されます。

### <a name="maximum-worker-threads"></a>[ワーカー スレッドの最大数]
0 を指定すると、SQL Server によってワーカー スレッドの数が動的に設定されます。 この設定は、ほとんどのシステムで最適な設定です。 ただし、システム構成によっては、このオプションに特定の値を設定した方がパフォーマンスが向上することがあります。 詳細については、「 [max worker threads サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)」を参照してください。  

### <a name="boost-sql-server-priority"></a>SQL Server の優先度を上げる
Microsoft Windows スケジュールでの SQL Server の優先度を、同じコンピューター内の他のプロセスよりも高くして実行するかどうかを指定します。 詳細については、「 [priority boost サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)」を参照してください。  

> [!Note]
> このオプションは、SSMS 18.x 以降のバージョンでは使用できません。

### <a name="use-windows-fibers-lightweight-pooling"></a>[Windows ファイバーを使用する (簡易プーリング)]
SQL Server サービスに対して、スレッドの代わりに Windows ファイバーを使用します。 これは、Windows 2003 Server Edition でのみ使用できます。 詳細については、「 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)」を参照してください。

> [!Note]
> このオプションは、SSMS 18.x 以降のバージョンでは使用できません。

### <a name="configured-values"></a>[構成した値]
このペインの各オプションに構成されている値を表示します。 これらの値を変更した場合は、 **[実行中の値]** を選択して、変更後の値が反映されているかどうかを確認してください。 そうなっていない場合は、最初に SQL Server のインスタンスを再起動する必要があります。

### <a name="running-values"></a>[実行中の値]
このペイン上のオプションの、現在実行中の値を表示します。 これらの値は読み取り専用です。

## <a name="see-also"></a>参照
[サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  


