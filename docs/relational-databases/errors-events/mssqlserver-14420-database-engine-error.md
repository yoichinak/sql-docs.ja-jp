---
description: MSSQLSERVER_14420
title: MSSQLSERVER_14420 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 14420 (Database Engine error)
ms.assetid: 4a1d72b1-ab1b-4119-a11b-a8a05c6fdb45
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 908c2726504def18fd2d737595a46d276eda1069
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88334668"
---
# <a name="mssqlserver_14420"></a>MSSQLSERVER_14420
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|14420|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum14420|  
|メッセージ テキスト|ログ配布プライマリ データベース %s.%s では、バックアップのしきい値が %d 分間ですが、%d 分間バックアップ ログ操作が実行されていません。 エージェント ログおよびログ配布モニターの情報を調べてください。|  
  
## <a name="explanation"></a>説明  
バックアップのしきい値を超えましたが、ログ配布が同期されていません。 バックアップのしきい値は、ログ配布のバックアップが完了するまでの許容時間 (分数) です。この時間が経過すると警告が生成されます。 このメッセージは、必ずしもログ配布に関する問題を示しません。 このメッセージは次の問題のいずれかを示す可能性があります。  
  
-   バックアップ ジョブが実行されていない。 原因として、プライマリ サーバー インスタンスで SQL Server エージェント サービスが実行されていないか、バックアップ ジョブが無効になっているか、またはバックアップ ジョブのスケジュールが変更されていることが考えられます。  
  
-   バックアップ ジョブが失敗している。 原因として、バックアップ フォルダーのパスが有効でないか、ディスクがいっぱいになっているか、またはその他の理由で BACKUP ステートメントが失敗したことが考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
このメッセージが表示された場合は、次の方法で対処してください。  
  
-   プライマリ サーバー インスタンスで SQL Server エージェント サービスが実行されていることを確認します。また、プライマリ データベースのバックアップ ジョブが有効になっており、適切な頻度で実行するようにスケジュール設定されていることを確認します。  
  
-   プライマリ サーバーのバックアップ ジョブが失敗している可能性があります。 この場合は、バックアップ ジョブのジョブ履歴を参照して原因を探してください。  
  
-   プライマリ サーバー インスタンスでログ配布のバックアップ ジョブを実行する際、監視サーバー インスタンスに接続して **log_shipping_monitor_primary** テーブルを更新できない可能性があります。 その場合、監視サーバー インスタンスとプライマリ サーバー インスタンス間での認証に問題があると思われます。  
  
-   バックアップの警告のしきい値に、正しくない値が設定されている可能性があります。 この値は、バックアップ ジョブの少なくとも 3 倍の頻度に設定するのが理想的です。 ログ配布を構成し、有効にした後で、バックアップ ジョブの頻度を変更した場合は、それに合わせてバックアップの警告しきい値も更新する必要があります。  
  
-   監視サーバー インスタンスがオフラインになり、その後オンラインに戻ったとき、警告メッセージ ジョブが実行される前に、**log_shipping_monitor_primary** テーブルが現在の値に更新されません。 監視テーブルを更新して、プライマリ データベースの最新データを反映させるには、プライマリ サーバー インスタンスで **sp_refresh_log_shipping_monitor** を実行します。  
  
-   プライマリ サーバー インスタンスまたは監視サーバー インスタンスで、日付または時刻が正しく設定されていません。 これが原因で、警告メッセージが生成される場合もあります。 これらいずれかのサーバーで、システムの日付または時刻が変更された可能性があります。  
  
    > [!NOTE]  
    > 2 つのサーバー インスタンスでタイム ゾーンが異なることによって、問題が発生することはありません。  
  
## <a name="see-also"></a>参照  
[log_shipping_monitor_primary &#40;Transact-SQL&#41;](~/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)  
[ログ配布について &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
[sp_help_log_shipping_monitor_primary &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)  
[sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)  
[ログ配布について &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
