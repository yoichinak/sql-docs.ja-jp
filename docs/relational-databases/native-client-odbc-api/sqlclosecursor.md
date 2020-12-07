---
description: SQLCloseCursor
title: 'Sqlclo: |Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e5f1e64174ead159c6a7d8b6f5704be18ee1129
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811124"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SqlcloSQLFreeStmt**は、 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) *オプション*の値を SQL_CLOSE に置き換えます。 Native Client ODBC ドライバーでは、 **Sqlcloの**受信時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保留中の結果セットの行が破棄されます。 ステートメントの列とパラメーターのバインド (存在する場合) は、 **Sqlcloに**よって変更されないことに注意してください。  
  
## <a name="see-also"></a>参照  
 [SQLCloseCursor]()   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
