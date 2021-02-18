---
title: トレースを一時停止する
titleSuffix: SQL Server Profiler
description: SQL Server Profiler によるイベント データのキャプチャが停止するよう、トレースを一時停止する方法と、トレースの一時停止中に変更できるプロパティについて説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 4c87c6d92edfaab6da1dac5d912db8a82fbfb4cf
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100353406"
---
# <a name="pause-a-trace-sql-server-profiler"></a>トレースの一時停止 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
トレースを一時停止すると、トレースを再開するまで、それ以上のイベント データはキャプチャされません。  
  
 トレースを一時停止すると、トレースを再開するまで、それ以上のイベント データはキャプチャされません。 トレースを再開すると、トレース操作が再開されます。 キャプチャを再開しても、それ以前にキャプチャしたデータが失われることはありません。 トレースを再開すると、その時点から、データのキャプチャが再開されます。 トレースを一時停止している間は、名前、イベント、列、およびフィルターを変更することができます。 ただし、トレース データの送信先またはサーバー接続は変更できません。  
  
### <a name="to-pause-a-trace"></a>トレースを一時停止するには  
  
1.  実行中のトレースを含んでいるウィンドウを選択します。  
  
2.  **[ファイル]** メニューの **[トレースの一時停止]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
