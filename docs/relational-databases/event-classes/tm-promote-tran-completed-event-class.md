---
description: 'TM: Promote Tran Completed イベント クラス'
title: 'TM: Promote Tran Completed イベント クラス | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 'TM: Promote Tran Completed event class'
ms.assetid: 839beaed-b094-467a-9b97-8764e9451fc0
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fa1538e08e6c404b87055051e667199033006cf2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470650"
---
# <a name="tm-promote-tran-completed-event-class"></a>TM: Promote Tran Completed イベント クラス
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  TM: Promote Tran Completed イベント クラスは、PROMOTE TRANSACTION 要求が完了したことを示します。 要求は、トランザクション管理インターフェイスを使用してクライアントから送信されます。  
  
## <a name="tm-promote-tran-completed-event-class-data-columns"></a>TM: Promote Tran Completed イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|BinaryData|**image**|DTC トランザクションのトークン。|2|はい|  
|ClientProcessID|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|DatabaseID|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|エラー|**int**|特定のイベントのエラー番号。 多くの場合、sys.messages カタログ ビューに保存されているエラー番号です。|31|はい|  
|EventClass|**int**|イベントの種類 = 184。|27|いいえ|  
|EventSequence|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|GroupID|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LoginName|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSid|**image**|ログインしたユーザーのセキュリティ識別子 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NTDomainName|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|**nvarchar**|Windows のユーザー名。|6|はい|  
|RequestID|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|ServerName|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|**int**|イベントが発生したセッションの ID。|12|はい|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|Success|**int**|1 = 成功。 0 = 失敗 (たとえば、値が 1 の場合は権限チェックの成功を表し、値が 0 の場合は失敗を表します)。|23|はい|  
|TransactionID|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|XactSequence|**bigint**|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
