---
description: SQLFreeStmt
title: SQLFreeStmt |Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a131178ecef5a9a0e04eb1b0564f89e6788d745
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811096"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  一般的に   
      **SQLFreeStmt** は、ODBC 3.0 以降では推奨されません。 ただし、アプリケーションでステートメントを再利用する必要がある場合でも、 **SQL_RESET_PARAMS**と**SQL_UNBIND**のオプションを指定して**SQLFreeStmt**を使用する必要があります。 [SqlcloSQLBindParameter](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)、 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)、 [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)、および[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) [sqlfreehandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)を使用して、 **SQLFreeStmt**の関数を置き換えたり複製したりすることもできます。代わりに、これらの関数を使用する必要があります。  
  
 一般に、ステートメントを再利用して新しいステートメントを割り当てるよりも効率的です。 ただし、ステートメントを再利用する場合のように、SQLFreeStmt を使用する必要がある場合もあります。  
  
## <a name="see-also"></a>参照  
 [SQLFreeStmt 関数](../../odbc/reference/syntax/sqlfreestmt-function.md)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
