---
description: dm_tran_transactions_snapshot (Transact-sql)
title: dm_tran_transactions_snapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_transactions_snapshot
- dm_tran_transactions_snapshot
- sys.dm_tran_transactions_snapshot_TSQL
- dm_tran_transactions_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_transactions_snapshot dynamic management view
ms.assetid: 03f64883-07ad-4092-8be0-31973348c647
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bb750ba886aeddc9871e9b3fdbc6d020b9839079
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546442"
---
# <a name="sysdm_tran_transactions_snapshot-transact-sql"></a>dm_tran_transactions_snapshot (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  各スナップショットトランザクションの開始時にアクティブになっているトランザクションの **sequence_number** の仮想テーブルを返します。 このビューで返される情報を基に、次のことを確認できます。  
  
-   現在アクティブなスナップショットトランザクションの数を調べます。  
  
-   特定のスナップショット トランザクションで無視されるデータ変更。 スナップショットトランザクションの開始時にアクティブなトランザクションの場合、そのトランザクションによって行われたすべてのデータ変更は、そのトランザクションがコミットした後でも、スナップショットトランザクションによって無視されます。  
  
 たとえば、 **dm_tran_transactions_snapshot**からの次の出力を考えてみます。  
  
```  
transaction_sequence_num snapshot_id snapshot_sequence_num  
------------------------ ----------- ---------------------  
59                       0           57  
59                       0           58  
60                       0           57  
60                       0           58  
60                       0           59  
60                       3           57  
60                       3           58  
60                       3           59  
60                       3           60  
```  
  
 `transaction_sequence_num` 列は、現在のスナップショット トランザクションのトランザクション シーケンス番号 (XSN) です。 出力には、との2つが示されて `59` `60` います。 `snapshot_sequence_num` 列は、各スナップショット トランザクションの開始時にアクティブ状態にあったトランザクションのトランザクション シーケンス番号です。  
  
 出力には、2つのアクティブなトランザクション (XSN-57 と XSN-58) が実行されている間にスナップショットトランザクション XSN-59 が開始されることが示されています。 XSN-57 または XSN-58 によってデータが変更された場合、XSN-59 では変更が無視され、行のバージョン管理を使用してデータベースのトランザクション上の一貫性のあるビューが維持されます。  
  
 スナップショットトランザクション XSN-60 では、xsn-57 と XSN-58 および XSN 59 によって行われたデータ変更は無視されます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|スナップショットトランザクションのトランザクションシーケンス番号 (XSN)。|  
|**snapshot_id**|**int**|各ステートメントのスナップショット ID は [!INCLUDE[tsql](../../includes/tsql-md.md)] 、行のバージョン管理を使用して read committed で開始されます。 この値は、行のバージョン管理を使用して read committed で実行されている各クエリをサポートする、トランザクション上一貫性のあるデータベースのビューを生成するために使用されます。|  
|**snapshot_sequence_num**|**bigint**|スナップショット トランザクションが開始したときに有効となっていたトランザクション シーケンス番号。|  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="remarks"></a>解説  
 スナップショットトランザクションが開始されると、その [!INCLUDE[ssDE](../../includes/ssde-md.md)] 時点でアクティブになっているすべてのトランザクションがによって記録されます。 dm_tran_transactions_snapshot は、現在アクティブなすべてのスナップショットトランザクションについて、この情報を報告し**ます。**  
  
 各トランザクションは、トランザクションの開始時に割り当てられたトランザクションシーケンス番号によって識別されます。 トランザクションは、BEGIN TRANSACTION または BEGIN WORK ステートメントが実行されたときに開始されますが、 トランザクション シーケンス番号は、BEGIN TRANSACTION または BEGIN WORK ステートメントの後、最初にデータにアクセスする [!INCLUDE[ssDE](../../includes/ssde-md.md)] ステートメントが実行されたときに[!INCLUDE[tsql](../../includes/tsql-md.md)]によって割り当てられます。 トランザクション シーケンス番号は 1 ずつ増加します。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

