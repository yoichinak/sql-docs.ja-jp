---
description: CPU のアイドル時間と期間の設定
title: CPU のアイドル時間と期間の設定
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CPU [SQL Server], idle conditions
- time [SQL Server], CPU idle and duration
- duration of CPU idle [SQL Server]
- SQL Server Agent, CPU idle conditions
- idle time [SQL Server]
ms.assetid: 8647b465-d899-4cc7-9640-134a506d0a2e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ab8d7167e81b5a7cdf665f1312b1b414d95d9f7b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037793"
---
# <a name="set-cpu-idle-time-and-duration"></a>CPU のアイドル時間と期間の設定

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、サーバーの CPU アイドル状態を定義する方法について説明します。 CPU アイドルの定義は、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがイベントに応答する方法に影響します。 たとえば、CPU の平均使用率が 10% 未満になり、そのレベルで 10 分間経過したときを CPU アイドル状態であると定義するとします。 この場合に、サーバーの CPU がアイドル状態になるたびにジョブが実行されるように定義していると、CPU 使用率が 10% 未満になり、その使用率のまま 10 分間経過したときにジョブが開始されます。 このジョブがサーバーのパフォーマンスに大きな影響を及ぼす場合、CPU アイドル状態をどのように定義するかが重要になります。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-set-cpu-idle-time-and-duration"></a>CPU のアイドル時間と期間を設定するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックして、 **[詳細設定]** ページをクリックします。  
  
3.  **[CPU のアイドル状態]** で、次の操作を行います。  
  
    -   **[CPU のアイドル状態を定義する]** チェック ボックスをオンにします。  
  
    -   **[CPU の平均使用量が次の値以下になったとき]** ボックスで、比率を指定します (全 CPU 共通)。 これにより、CPU がその値を下回ったときにアイドル状態と見なす使用率が設定されます。  
  
    -   **[かつ、この使用率以下で次の期間を経過]** ボックスで、秒数を指定します。 低い CPU 使用率のまま、ここで設定した秒数が経過すると、CPU がアイドル状態であると見なされます。  
