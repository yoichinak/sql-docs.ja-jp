---
description: sys.dm_tcp_listener_states (Transact-SQL)
title: dm_tcp_listener_states (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tcp_listener_states
- dm_tcp_listener_states
- sys.dm_tcp_listener_states_TSQL
- dm_tcp_listener_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.dm_tcp_listener_states dynamic management view
ms.assetid: 9997ffed-a4c1-428f-8bac-3b9e4b16d7cf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4da7c8a5c8cfd87ae0c1ffa4216996e1d9e0413a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550174"
---
# <a name="sysdm_tcp_listener_states-transact-sql"></a>sys.dm_tcp_listener_states (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  各 TCP リスナーの動的状態情報を含む行を返します。  
  
> [!NOTE]
> 可用性グループ リスナーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのリスナーと同じポートでリッスンしている場合があります。 この場合、リスナーは、Service Broker リスナーの場合と同じように、個別に一覧表示されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**listener_id**|**int**|リスナーの内部 ID。 NULL 値は許可されません。<br /><br /> 主キー|  
|**ip_address**|**nvarchar (48)**|オンラインであり、現在リッスンしているリスナーの IP アドレス。 IPv4 と IPv6 のどちらかを使用できます。 リスナーが両方の種類のアドレスを所有している場合は、個別に一覧表示されます。 IPv4 のワイルドカードは、"0.0.0.0" と表示されます。 IPv6 ワイルドカードは、"::" として表示されます。<br /><br /> NULL 値は許可されません。|  
|**is_ipv4**|**bit**|IP アドレスの種類<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
|**port**|**int**|リスナーがリッスンしているポート番号。 NULL 値は許可されません。|  
|**type**|**tinyint**|リスナーの種類。次のいずれかになります。<br /><br /> 0 = [!INCLUDE[tsql](../../includes/tsql-md.md)]<br /><br /> 1 = Service Broker<br /><br /> 2 = データベースミラーリング<br /><br /> NULL 値は許可されません。|  
|**type_desc**|**nvarchar (20)**|**型**の説明。次のいずれかになります。<br /><br /> TSQL<br /><br /> SERVICE_BROKER<br /><br /> DATABASE_MIRRORING<br /><br /> NULL 値は許可されません。|  
|**状態**|**tinyint**|可用性グループのリスナーの状態。次のいずれかになります。<br /><br /> 1 = オンライン。 リスナーが要求のリスニングおよび処理中です。<br /><br /> 2 = 再起動の保留中。 リスナーはオフラインであり、再起動が保留されています。<br /><br /> 可用性グループリスナーがサーバーインスタンスと同じポートをリッスンしている場合、これら2つのリスナーは常に同じ状態になります。<br /><br /> NULL 値は許可されません。<br /><br /> 注: この列の値は、TSD_listener オブジェクトから取得されます。 TDS_listener がオフラインの場合は状態をクエリできないため、この列ではオフライン状態はサポートされていません。|  
|**state_desc**|**nvarchar (16)**|**状態**の説明。次のいずれかになります。<br /><br /> ONLINE<br /><br /> PENDING_RESTART<br /><br /> NULL 値は許可されません。|  
|**start_time**|**datetime**|リスナーが開始された日時を示すタイムスタンプ。 NULL 値は許可されません。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [SQL Server システムカタログに対するクエリについてよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [AlwaysOn 可用性グループの動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
