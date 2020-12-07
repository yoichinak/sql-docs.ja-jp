---
description: sys.dm_external_script_execution_stats
title: sys. dm_external_script_execution_stats |Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_execution_stats
- sys.dm_external_script_execution_stats_TSQL
- dm_external_script_execution_stats
- dm_external_script_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_execution_stats dynamic management view
ms.assetid: 2e99f026-ceb2-42a2-a549-c71d31ed0cf4
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 9c8244de0efc2bdd3dc506e5e1ebcddcd4843dea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489925"
---
# <a name="sysdm_external_script_execution_stats"></a>sys.dm_external_script_execution_stats
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

外部スクリプト要求の種類ごとに 1 つの行を返します。 外部スクリプト要求は、サポートされている外部スクリプト言語でグループ化されます。 登録されている外部スクリプト関数ごとに 1 つの行が生成されます。 `rxExec`など、任意の外部スクリプト関数は、親プロセスによって送信された場合を除き、記録されません。
  
> [!NOTE]  
> この動的管理ビュー (DMV) は、外部スクリプトの実行をサポートする機能をインストールして有効にした場合にのみ使用できます。 詳細については、SQL Server 2017 以降および[Azure Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)での[SQL Server 2016 の r Services](../../machine-learning/r/sql-server-r-services.md)、 [Machine Learning Services (r、Python)](../../machine-learning/sql-server-machine-learning-services.md) 」を参照してください。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|language|**nvarchar**|登録されている外部スクリプト言語の名前です。 各外部スクリプトは、スクリプト要求で言語を指定して、関連付けられているランチャーを開始する必要があります。 |  
|counter_name|**nvarchar**|登録されている外部スクリプト関数の名前です。 NULL 値は許可されません。|  
|counter_value|**integer**|登録されている外部スクリプト関数がサーバーで呼び出されたインスタンスの合計数です。 この値は、機能がインスタンスにインストールされてからの累積値で、リセットすることはできません。|  

## <a name="permissions"></a>アクセス許可

 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
> [!NOTE]  
> 外部スクリプトを実行するユーザーはさらに EXECUTE ANY EXTERNAL SCRIPT 権限も持っている必要がありますが、管理者はこの権限がなくてもこの DMV を使用できます。
  
## <a name="remarks"></a>解説

  この DMV は、 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]で提供される新しい外部スクリプト実行機能の全体的な使用状況を監視するために、内部テレメトリ用に提供されます。 登録されている外部スクリプト関数が呼び出されるたびにスタート パッドがディスクベースのカウンターを増分すると、テレメトリ サービスが開始します。

一般に、パフォーマンス カウンターは、それを生成したプロセスがアクティブな間だけ有効です。 したがって、DMV に対するクエリは、実行を停止したサービスの詳細なデータを表示できません。 たとえば、ランチャーが外部スクリプトを実行しても、すぐに完了した場合、従来の DMV ではデータが表示されない可能性があります。

したがって、インスタンスがシャットダウンされた場合でも、この DMV によって追跡されるカウンターは実行状態を維持し、sys.dm_external_script_requests の状態はディスクへの書き込みを使用して保持されます。

### <a name="counter-values"></a>カウンターの値

SQL Server 2016 では、サポートされている外部言語は R だけで、外部スクリプト要求はによって処理され [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] ます。 2017以降、および Azure SQL Managed Instance では、R と Python の両方がサポートされている外部言語と、外部スクリプト要求はによって処理され [!INCLUDE[rsql_productname_md](../../includes/rsql-productnamenew-md.md)] ます。 SQL Server

R の場合、この DMV はインスタンスに対して行われた R 呼び出しの数を追跡します。 たとえば、 `rxLinMod` が呼び出されて並列で実行された場合、このカウンターは 1 だけ増やされます。

R 言語の場合、 *counter_name* フィールドに表示されるカウンターの値は、登録されている ScaleR 関数の名前を表します。 *counter_value* フィールドの値は、特定の ScaleR 関数を呼び出したインスタンスの累積数を表します。 

Python の場合、この DMV はインスタンスに対して行われた Python 呼び出しの数を追跡します。

インスタンスで機能がインストールされて有効にされるとカウントが開始し、状態を保持しているファイルが削除されるか、管理者によって上書きされるまで、カウントは累積されます。 したがって、 *counter_value*の値をリセットすることは通常は不可能です。 セッション、カレンダーの時間、またはその他の間隔で使用状況を監視する必要がある場合は、カウントをテーブルに取得することをお勧めします。

### <a name="registration-of-external-script-functions-in-r"></a>R での外部スクリプト関数の登録

R は任意のスクリプトをサポートしており、R コミュニティでは、それぞれ独自の関数とメソッドを使用して、数千のパッケージが提供されています。 ただし、この DMV は SQL Server 2016 R Services と共にインストールされた ScaleR 関数のみを監視します。

これらの関数の登録は機能がインストールされると実行され、登録された関数を追加または削除することはできません。

## <a name="examples"></a>例  
  
### <a name="viewing-the-number-of-r-scripts-run-on-the-server"></a>サーバー上で実行されている R スクリプトの数を表示する

 次の例は、R 言語の外部スクリプト実行の累積数を表示します。  
  
```sql
SELECT counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE language = 'R';
```  

### <a name="viewing-the-number-of-python-scripts-run-on-the-server"></a>サーバーで実行される Python スクリプトの数を表示する

次の例では、Python 言語の外部スクリプト実行の累積数を表示します。  
  
```sql
SELECT counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE language = 'Python';
```  

## <a name="see-also"></a>関連項目

+ [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
