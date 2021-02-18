---
title: Transact-SQL スクリプトを再生する
titleSuffix: SQL Server Profiler
description: SQL Server Profiler を使用して Transact-SQL スクリプトを再生し、さまざまな解決策とパフォーマンスの問題を比較できるようにする方法について説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 20252994f90032293730335dda1f6dd689133497
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100353437"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Transact-SQL スクリプトの再生 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

パフォーマンスの問題に対して考えられる解決策をテストする場合、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを再生し、変更を加える前と加えた後のパフォーマンスを比較します。  
  
### <a name="to-replay-a-transact-sql-script"></a>Transact-SQL スクリプトを再生するには  
  
1.  **[ファイル]** メニューの **[開く]** をポイントし、 **[スクリプト ファイル]** をクリックします。  
  
2.  [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイルを選択して開きます。 再生に必要なイベントが [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトに含まれていることを確認してください。 詳細については、「 [再生を実行するための必要条件](../../tools/sql-server-profiler/replay-requirements.md)」を参照してください。  
  
3.  **[再生]** メニューの **[開始]** をクリックし、スクリプトを再生するサーバーに接続します。  
  
4.  **[構成の再生]** ダイアログ ボックスで設定を確認し、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [トレースの再生](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
