---
description: MSSQL_ENG014163
title: MSSQL_ENG014163 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- MSSQL_ENG014163 error
ms.assetid: b53dd463-ba36-421e-9745-67c7387e68dd
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 953801b4bbfaa96ccaee971d6a65461579642e00
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191620"
---
# <a name="mssql_eng014163"></a>MSSQL_ENG014163
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|属性|値|  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14163|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 マージ エージェントが実行されており、必要な要件に適合することを確認してください。|  
  
## <a name="explanation"></a>説明  
 レプリケーションでは、いくつかの条件に対して警告を有効にできます。 たとえば、マージ パブリッシャーとサブスクライバーの間で変更を同期する時間が指定の長さを超えた場合などです。 LAN 接続とダイヤルアップ接続には異なる時間を指定できます。  
  
 レプリケーション モニターまたは [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)を使用して警告を有効にするときは、警告を表示するタイミングを決定するしきい値を指定します。 指定したしきい値に達するか、そのしきい値を超えた場合、警告がレプリケーション モニターに表示され、イベントが Windows イベント ログに書き込まれます。 しきい値に達した時点で、SQL Server エージェントの警告を表示させることもできます。 詳細については、「[レプリケーション モニターのしきい値と警告の設定](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)」および「[プログラムによるレプリケーションの監視](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 サブスクリプションが期間のしきい値を超えた場合は、システムでパフォーマンスの問題が発生しているかどうか、またはしきい値を調整する必要があるかどうかを確認する必要があります。 レプリケーションを構成したら、パフォーマンス基準を策定します。これにより、アプリケーションおよびトポロジにおける通常のワークロードに対するレプリケーションの動作方法について判断できるようになります。 このパフォーマンス基準には同期の期間を組み入れ、適切なしきい値を設定できるようにします。  
  
 しきい値が適切でも、その値を超えた場合は、システム内のパフォーマンスのボトルネックになる部分を特定する必要があります。 レプリケーション パフォーマンスの監視とトラブルシューティングを行う方法の詳細については、「[レプリケーション モニターを使用したパフォーマンスの監視](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
