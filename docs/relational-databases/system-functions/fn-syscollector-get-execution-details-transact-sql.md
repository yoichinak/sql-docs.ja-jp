---
description: fn_syscollector_get_execution_details (Transact-SQL)
title: fn_syscollector_get_execution_details (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_details_TSQL
- fn_syscollector_get_execution_details
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_details function
ms.assetid: d59ddf0c-72c0-4c57-bc83-aef260e4e105
author: rothja
ms.author: jroth
ms.openlocfilehash: 615dd195f9553242b92b8830462036ab6384b665
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474666"
---
# <a name="fn_syscollector_get_execution_details-transact-sql"></a>fn_syscollector_get_execution_details (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssIS](../../includes/ssis-md.md)] ログ (sysssislog) で、指定されたパッケージの package_execution_id と一致する部分を返します。 このテーブルには、パッケージまたはパッケージのタスクとコンテナーによって実行時に生成されるログエントリごとに1行のレコードが含まれています。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_syscollector_get_execution_details ( log_id )  
```  
  
## <a name="arguments"></a>引数  
 *log_id*  
 実行ログの一意なローカル識別子を指定します。 *log_id* は **int**です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**int**|ログエントリの一意の識別子。|  
|event|**sysname**|ログ エントリを生成したイベントの名前。|  
|コンピュータ|**nvarchar**|ログ エントリの生成時にパッケージが実行されていたコンピューター。|  
|operator|**nvarchar**|ログエントリを生成したパッケージを実行したユーザーまたはエージェントのユーザー名。|  
|source|**nvarchar**|ログエントリを生成した実行可能ファイルの名前。|  
|sourceid|**uniqueidentifier**|ログエントリを生成した実行可能ファイルの GUID。|  
|executionid|**uniqueidentifier**|ログエントリを生成した実行可能ファイルの実行インスタンスの GUID。|  
|starttime|**datetime**|パッケージの実行が開始された時刻です。|  
|endtime|**datetime**|パッケージが完了した時刻です。|  
|datacode|**int**|ログエントリに関連付けられたイベントを識別する整数値です。 "0" は、イベントで識別子が指定されていないことを示します。|  
|databytes|**image**|戻り値を識別するバイト配列。|  
|message|**nvarchar**|イベントの説明とイベントに関連付けられている情報。|  
  
## <a name="permissions"></a>アクセス許可  
 **Dc_operator**に対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [SQL Server Data Tools でパッケージのログ記録を有効にする](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
