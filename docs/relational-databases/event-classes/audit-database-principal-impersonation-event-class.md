---
description: Audit Database Principal Impersonation イベント クラス
title: Audit Database Principal Impersonation イベント クラス
ms.date: 06/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Audit Database Principal Impersonation event class
ms.assetid: 1b29dea4-3727-4c5f-8362-4ca0374de0b6
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 2daffee015f4abb0f102f9ddb7f9c50af8444be8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88384848"
---
# <a name="audit-database-principal-impersonation-event-class"></a>Audit Database Principal Impersonation イベント クラス
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **Audit Database Principal Impersonation** イベント クラスは、EXECUTE AS \<*user*> や SETUSER などのデータベース スコープ内で権限の借用が生じるときに発生します。  
  
## <a name="audit-database-principal-impersonation-event-class-data-columns"></a>Audit Database Principal Impersonation イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|**DBUserName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー名。|40|はい|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**EventSubClass**|**int**|イベント サブクラスの種類。|21|はい|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログイン、または DOMAIN\username の形式で表された [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 **sys.server_principals** カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**ObjectName**|**nvarchar**|参照されているオブジェクトの名前。|34|はい|  
|**ObjectType**|**int**|イベントに関係するオブジェクトの種類を表す値。 この値は **sys.objects** カタログ ビューの type 列に対応します。 値については、「 [ObjectType トレース イベント列](../../relational-databases/event-classes/objecttype-trace-event-column.md)」を参照してください。|28|はい|  
|**アクセス許可**|**bigint**|チェックする権限の種類を表す整数値。<br /><br /> 1 = SELECT ALL<br /><br /> 2 = UPDATE ALL<br /><br /> 4 = REFERENCES ALL<br /><br /> 8 = INSERT<br /><br /> 16 = DELETE<br /><br /> 32 = EXECUTE (プロシージャのみ)|19|はい|  
|**RequestID**|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|**RoleName**|**nvarchar**|有効にするアプリケーション ロールの名前。|38|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**Success**|**int**|1 = 成功。 0 = 失敗。 たとえば、値 1 は権限チェックの成功を示し、値 0 は失敗を示します。|23|はい|  
|**TextData**|**ntext**|トレースでキャプチャされたイベント クラスに依存するテキスト値。|1|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|**XactSequence**|**bigint**|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [EXECUTE AS 句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [SETUSER &#40;Transact-SQL&#41;](../../t-sql/statements/setuser-transact-sql.md)  
  
  
