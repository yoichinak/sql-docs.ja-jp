---
description: SQLSetEnvAttr
title: SQLSetEnvAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c18b93ba462e35be1f8bc34f85fed3297c05f964
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868460"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Odbc [プログラマーズリファレンス](../../odbc/reference/odbc-programmer-s-reference.md) では、odbc ドライバーが odbc 2 に書き込まれたアプリケーションから **SQLSetEnvAttr** 属性の仕様を解釈する方法を定義します。*x* または ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC ドライバーは、これらの規則に準拠しています。  
  
 **SQLSetEnvAttr**によって制御される属性の1つは、接続プールを使用するかどうかです。 Native Client ODBC ドライバーで接続プールを使用する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)または**SQLConnect**を使用して接続するときに、 *drivercompletion*パラメーターを SQL_DRIVER_NOPROMPT に設定する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQLSetEnvAttr 関数](../../odbc/reference/syntax/sqlsetenvattr-function.md)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
