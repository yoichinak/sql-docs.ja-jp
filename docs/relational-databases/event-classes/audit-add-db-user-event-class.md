---
description: Audit Add DB User イベント クラス
title: Audit Add DB User イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Audit Add DB User event class
ms.assetid: ac9ed573-c84d-444c-81fb-923a6240c1ef
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b953d49716cb6a99879ebc94c750fc1e765916e8
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128791"
---
# <a name="audit-add-db-user-event-class"></a>Audit Add DB User イベント クラス

[!INCLUDE [sql-asdb.md](../../includes/applies-to-version/sql-asdb.md)]

  **Audit Add DB User** イベント クラスは、データベースにデータベース ユーザーとしてログインが追加または削除されるたびに発生します。 このイベント クラスは、 **sp_grantdbaccess**、 **sp_revokedbaccess**、 **sp_adduser**、および **sp_dropuser** プロシージャに対して使用します。  
  
 このイベント クラスは、今後のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で廃止される可能性があります。 代わりに、 **Audit Database Principal Management** イベント クラスを使用することをお勧めします。  
  
## <a name="audit-add-db-user-event-class-data-columns"></a>Audit Add DB User イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|**ColumnPermissions**|**int**|列権限が設定されているかどうかのインジケーター。 ステートメントのテキストを解析して、どの権限がどの列に適用されていたかを判断します。|44|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**DatabaseName**|**nvarchar**|ユーザー名が追加または削除されたデータベースの名前。|35|はい|  
|**DBUserName**|**nvarchar**|データベース内の発行者のユーザー名。|40|はい|  
|**EventClass**|**int**|イベントの種類 = 109。|27|いいえ|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**EventSubClass**|**int**|イベント サブクラスの種類。<br /><br /> 1 = 追加<br /><br /> 2 = 削除<br /><br /> 3 = データベース アクセスの許可<br /><br /> 4 = データベース アクセスの禁止|21|はい|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログイン、または DOMAIN\username の形式で表された [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 **sys.server_principals** カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**OwnerName**|**nvarchar**|オブジェクト所有者のデータベース ユーザー名。|37|はい|  
|**RequestID**|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|**RoleName**|**nvarchar**|メンバーが変更されたデータベース ロールの名前 ( **sp_adduser** を使用した場合)。|38|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26||  
|**SessionLoginName**|**Nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**Success**|**int**|1 = 成功。 0 = 失敗。 たとえば、値 1 は権限チェックの成功を示し、値 0 は失敗を示します。|23|はい|  
|**TargetLoginName**|**nvarchar**|データベースへのアクセス権が変更されたログイン名。|42|はい|  
|**TargetLoginSid**|**image**|新しいログインの追加など、ログインを対象とする操作で、対象となるログインのセキュリティ識別番号 (SID)。|43|はい|  
|**TargetUserName**|**nvarchar**|ユーザーにより追加されたデータベース名。|39|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|**XactSequence**|**bigint**|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [Audit Database Principal Management イベント クラス](../../relational-databases/event-classes/audit-database-principal-management-event-class.md)  
  
  
