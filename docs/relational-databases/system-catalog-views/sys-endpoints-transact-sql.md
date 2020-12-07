---
description: sys.endpoints (Transact-SQL)
title: sys. エンドポイント (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- endpoints
- sys.endpoints
- endpoints_TSQL
- sys.endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoints catalog view
ms.assetid: e6dafa4e-e47e-43ec-acfc-88c0af53c1a1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 73555ee11e3f03c8478ca170039b7b367036fc4f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548761"
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  システム内に作成されるエンドポイントごとに1行のレコードを格納します。 システムエンドポイントは常に1つだけ存在します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|エンドポイントの名前。 はサーバー内で一意です。 NULL 値は許可されません。|  
|**endpoint_id**|**int**|エンドポイントの ID。 はサーバー内で一意です。 65536 より小さい ID のエンドポイントは、システム エンドポイントです。 NULL 値は許可されません。|  
|**principal_id**|**int**|このエンドポイントを作成して所有しているサーバープリンシパルの ID。 NULL 値が許可されます。|  
|**protocol**|**tinyint**|エンドポイントプロトコル。<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = 名前付きパイプ<br /><br /> 4 = 共有メモリ<br /><br /> 5 = 仮想インターフェイスアダプター (VIA)<br /><br /> NULL 値は許可されません。|  
|**protocol_desc**|**nvarchar(60)**|エンドポイントプロトコルの説明。 NULLABLE. 次のいずれかの値です。<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **VIA** 注: VIA プロトコルは非推奨とされます。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**type**|**tinyint**|エンドポイントのペイロードの種類。<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> NULL 値は許可されません。|  
|**type_desc**|**nvarchar(60)**|エンドポイントのペイロードの種類の説明。 NULL 値が許可されます。 次のいずれかの値です。<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**状態**|**tinyint**|エンドポイントの状態。<br /><br /> 0 = 要求を開始し、リッスンし、処理します。<br /><br /> 1 = 要求を停止、リッスン、処理していません。<br /><br /> 2 = 無効、リッスンしていません。<br /><br /> 既定の状態は1です。 NULL 値が許可されます。|  
|**state_desc**|**nvarchar(60)**|エンドポイントの状態の説明。<br /><br /> 開始 = 要求をリッスンして処理しています。<br /><br /> STOPPED = 要求のリスニング中で、処理は行っていません。<br /><br /> DISABLED = リッスンしていません。<br /><br /> 既定の状態は STOPPED です。<br /><br /> NULL 値が許可されます。|  
|**is_admin_endpoint**|**bit**|エンドポイントが管理用であるかどうかを示します。<br /><br /> 0 = 管理者用以外のエンドポイント。<br /><br /> 1 = エンドポイントは管理エンドポイントです。<br /><br /> NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
