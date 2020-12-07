---
title: MSpeer_conflictdetectionconfigresponse (T-sql)
description: ピアツーピアレプリケーションで、トポロジ全体の構成 requestion に対する各ノードの応答を格納するために使用される MSPeer_conflictdetectionconfigureresponse ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d402a77534b12fbb3bf880bcaac17be1dedcdde2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545572"
---
# <a name="mspeer_conflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  トポロジ全体の構成要求に対する各ノードの応答を保存するために、ピア ツー ピア レプリケーションで使用されます。 このテーブルは、パブリケーションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|request_id|**int**|[MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md)テーブルの競合構成要求エントリを識別します。|  
|peer_node|**sysname**|応答を生成したサーバーインスタンスの名前。|  
|peer_db|**sysname**|応答を生成したピアのサブスクリプションデータベース。|  
|peer_version|**sysname**|パブリッシャーのバージョン番号を識別します。|  
|peer_db_version|**sysname**|ピアデータベースのバージョン番号を識別します。|  
|is_peer|**bit**|ノードが読み取り専用のサブスクライバーであるかどうかを示します。 値が **0** の場合は、読み取り専用サブスクライバーを示します。|  
|conflict_detection_enabled|**bit**|トポロジで競合検出が有効になっているかどうかを示します。|  
|originator_id|**varbinary(16)**|競合検出のためにトポロジの各ノードを識別します。 詳細については、「 [ピア ツー ピア レプリケーションにおける競合検出](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。|  
|peer_conflict_retention|**int**|メタデータが競合テーブルに格納される期間 (日数)。|  
|peer_subscriptions|**XML**|要求に応答したノードに関する情報。|  
|progress_phase|**nvarchar(32)**|次のいずれかの値を使用して、処理の現在のフェーズを識別します。<br /><br /> Started<br /><br /> 収集されたピア バージョン<br /><br /> 収集された状態|  
|modified_date|**datetime**|フェーズが完了した日付と時刻。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
