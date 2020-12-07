---
title: SQL Server のメッセージ結果 (OLE DB ドライバー)
description: OLE DB Driver for SQL Server の行セットやカウント、および期待される戻り値を生成しない Transact-SQL ステートメントについて説明します。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc3701313f920eead650435ca40538ad8a4b6ef0
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862507"
---
# <a name="sql-server-message-results"></a>SQL Server のメッセージ結果
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントでは、OLE DB Driver for SQL Server の行セットや、ステートメント実行時に処理された行カウントは生成されません。  
  
-   PRINT  
  
-   重大度が 10 以下の RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 上記のステートメントでは、行セットや行数の結果が返されるのではなく、ステートメントから 1 つ以上の情報メッセージが返されるか、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から情報メッセージが返されます。 実行に成功すると、OLE DB Driver for SQL Server から S_OK が返され、OLE DB Driver for SQL Server コンシューマーはメッセージを利用できるようになります。  
  
 多くの [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントの実行後、またはコンシューマーでの OLE DB Driver for SQL Server のメンバー関数の実行後、OLE DB Driver for SQL Server は S_OK を返し、1 つまたは複数の情報メッセージが利用できるようになります。  
  
OLE DB Driver for SQL Server のコンシューマーは、クエリ テキストを動的に指定できます。 コンシューマーは、メンバー関数を実行する_たびに_エラー インターフェイスをチェックする必要があります。 これらのチェックは、リターン コードの値、`IRowset` または `IMultipleResults` へのインターフェイス参照が返されたかどうか、および処理された行数に関係なく、常に行う必要があります。
  
## <a name="see-also"></a>参照  
 [エラー](../../oledb/ole-db-errors/errors.md)  
  
  
