---
description: sys.dm_external_script_requests
title: sys. dm_external_script_requests |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_requests
- sys.dm_external_script_requests_TSQL
- dm_external_script_requests
- dm_external_script_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_requests dynamic management view
ms.assetid: e7e7c50f-b8b2-403c-b8c8-1955da5636c3
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 1b3c1f10be0b454503c5fbcfd9cdab191a687797
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489845"
---
# <a name="sysdm_external_script_requests"></a>sys.dm_external_script_requests
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

外部スクリプトを実行しているアクティブなワーカー アカウントごとに行を返します。
  
> [!NOTE]
> この動的管理ビュー (DMV) は、外部スクリプトの実行をサポートする機能をインストールして有効にした場合にのみ使用できます。 詳細については、 [SQL Server 2017 以降の Machine Learning Services (r、Python)](../../machine-learning/sql-server-machine-learning-services.md)、 [SQL Server 2016 の r Services](../../machine-learning/r/sql-server-r-services.md)、および [Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**一意識別子**|外部スクリプト要求を送信したプロセスの ID です。 これは、SQL インスタンスを受信したプロセス ID に対応します。|  
|language|**nvarchar**|サポートされているスクリプト言語を表すキーワードです。 |  
|degree_of_parallelism|**int**|作成された並列処理の数を示す数値です。 この値は、要求された並列処理の数と異なる場合があります。|  
|external_user_name|**nvarchar**|スクリプトが実行されたときの Windows ワーカー アカウント。|  
  
## <a name="permissions"></a>アクセス許可

 サーバーに対する権限が必要です `VIEW SERVER STATE` 。  
  
> [!NOTE]
> 外部スクリプトを実行するユーザーには、追加の権限が必要 `EXECUTE ANY EXTERNAL SCRIPT` です。ただし、この DMV は、管理者がこの権限なしで使用できます。 
  
## <a name="remarks"></a>解説  

このビューは、スクリプト言語の識別子を使用してフィルター処理することができます。

このビューはまた、スクリプトが実行されているワーカー アカウントも返します。 外部スクリプトによって使用されるワーカーアカウントの詳細については、 [SQL Server Machine Learning Services の機能拡張フレームワークのセキュリティの概要](../../machine-learning/concepts/security.md#sqlrusergroup)に関するトピックの「処理に使用される id」セクションを参照してください。

**external_script_request_id** フィールドに返される GUID はまた、一時ファイルが格納されている、セキュリティで保護されたディレクトリのファイル名も表します。 MSSQLSERVER01 などの各ワーカーアカウントは、単一の SQL ログインまたは Windows ユーザーを表し、複数のスクリプト要求を実行するために使用される場合があります。 既定では、これらの一時ファイルは、要求したスクリプトが完了するとクリーンアップされます。

この DMV は、アクティブなプロセスを監視するだけであり、既に完了しているスクリプトをレポートすることはできません。 スクリプトの期間を追跡する必要がある場合は、スクリプト内にタイミング情報を追加し、スクリプトの実行の一部としてキャプチャすることをお勧めします。

## <a name="examples"></a>例  
  
### <a name="viewing-the-currently-active-scripts-for-a-particular-process"></a>特定のプロセスに対して現在アクティブなスクリプトを表示する

 次の例では、現在のインスタンスで実行されている外部スクリプト実行の数を表示します。  
  
```sql
SELECT external_script_request_id
  , [language]
  , degree_of_parallelism
  , external_user_name
FROM sys.dm_external_script_requests;
```  

結果  

external_script_request_id  |language  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01

## <a name="see-also"></a>関連項目

+ [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
