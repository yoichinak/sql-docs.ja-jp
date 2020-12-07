---
description: SQLProcedures
title: SQLProcedures |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e535c47ec1dbcbb93314fc96f3435042495bec3a
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867749"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャは値を返します。 **Sqlprocedures** は、結果セット列 PROCEDURE_TYPE の SQL_PT_FUNCTION を報告します。  
  
 **Sqlprocedures** は *、CatalogName、SchemaName、* または *ProcName* パラメーターの値が存在するかどうかを SQL_SUCCESS 返します。 これらのパラメーターで無効な値が使用されている場合、 **Sqlfetch**は SQL_NO_DATA を返します。  
  
 **Sqlprocedures** は、静的サーバーカーソルで実行できます。 更新可能なカーソル (動的カーソルまたはキーセットカーソル) で **Sqlprocedures** を実行しようとすると、カーソルの種類が変更されたことを示す SQL_SUCCESS_WITH_INFO が返されます。  
  
 **Sqlprocedures** は、名前が *ProcName* に一致し、現在のユーザーが実行できる、または現在のユーザーが VIEW DEFINITION 権限を許可されているプロシージャに関する情報を返します。  
  
## <a name="see-also"></a>参照  
 [SQLProcedures 関数](../../odbc/reference/syntax/sqlprocedures-function.md)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
