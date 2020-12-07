---
description: データベースミラーリング監視サーバーのカタログビュー-sys. database_mirroring_witnesses
title: database_mirroring_witnesses (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_witnesses
- sys.database_mirroring_witnesses_TSQL
- database_mirroring_witnesses
- database_mirroring_witnesses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_witnesses catalog view
- witness [SQL Server], sys.database_mirroring_witnesses catalog view
ms.assetid: 0dd5b794-733b-4a3c-b5a4-62f9f1f0f22d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a321ea1734ce63941e2ba3ebac30bb0149891d09
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548832"
---
# <a name="database-mirroring-witness-catalog-views---sysdatabase_mirroring_witnesses"></a>データベースミラーリング監視サーバーのカタログビュー-sys. database_mirroring_witnesses
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーがデータベース ミラーリング パートナーシップで果たすすべてのミラーリング監視ロールの行を格納します。 
  
  データベース ミラーリング セッションで、自動フェールオーバーを行うには、ミラーリング監視サーバーが必要です。 ミラーリング監視サーバーは、プリンシパルサーバーとミラーサーバーの両方とは別のコンピューターに配置するのが理想的です。 ミラーリング監視サーバーは、データベースを提供しません。 代わりに、プリンシパルサーバーとミラーサーバーの状態を監視します。 プリンシパルサーバーで障害が発生した場合、ミラーリング監視サーバーはミラーサーバーへの自動フェールオーバーを開始できます。 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|データベースミラーリングセッションのデータベースの2つのコピーの名前。|  
|**principal_server_name**|**sysname**|現在データベースのコピーがプリンシパル データベースとなっているパートナー サーバーの名前。|  
|**mirror_server_name**|**sysname**|現在、データベースのコピーがミラーデータベースであるパートナーサーバーの名前。|  
|**safety_level**|**tinyint**|ミラーデータベースでの更新のトランザクションの安全性設定:<br /><br /> 0 = 状態不明<br /><br /> 1 = オフ (非同期)<br /><br /> 2 = 完全 (同期)<br /><br /> 自動フェールオーバーに対してミラーリング監視サーバーを使用する場合は、トランザクションの安全性が「完全」であること必要です。また、「完全」は既定の設定になっています。|  
|**safety_level_desc**|**nvarchar(60)**|ミラーデータベースに対する更新の安全性の保証の説明:<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL|  
|**safety_sequence_number**|**int**|**Safety_level**に対する変更のシーケンス番号を更新します。|  
|**role_sequence_number**|**int**|ミラーリングパートナーによって再生されるプリンシパル/ミラーロールに対する変更のシーケンス番号を更新します。|  
|**mirroring_guid**|**uniqueidentifier**|ミラーリングパートナーシップの識別子。|  
|**family_guid**|**uniqueidentifier**|データベースのバックアップファミリの識別子。 一致する復元状態を検出するために使用します。|  
|**is_suspended**|**bit**|データベース ミラーリングが一時中断していることを示す値。|  
|**is_suspended_sequence_number**|**int**|設定 **is_suspended**のシーケンス番号。|  
|**partner_sync_state**|**tinyint**|ミラーリングセッションの同期状態:<br /><br /> 5 = パートナーが同期されている。 フェールオーバーが可能な可能性があります。 フェールオーバーの要件の詳細については、「 [データベースミラーリングセッション中の役割の切り替え &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)」を参照してください。<br /><br /> 6 = パートナーが同期されていません。 現在、フェールオーバーは実行できません。|  
|**partner_sync_state_desc**|**nvarchar(60)**|ミラーリング セッションの同期状態の説明 :<br /><br /> SYNCHRONIZED<br /><br /> 非同期|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング監視サーバー](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [database_mirroring &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
