---
title: SQLSTATE (ODBC エラーコード) |Microsoft Docs
description: ODBC ドライバー SQL Server ストアドプロシージャをリモートストアドプロシージャとして実行する場合、プロシージャは整数のリターンコードと出力パラメーターを持つことができます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a358a3cd071c3b0a986925a1ef5fc181536283c0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868328"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC エラー コード)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SQLSTATE は、警告やエラーの原因についての詳細情報を提供します。 によって検出され、によって返されるデータソースで発生したエラーの場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC ドライバーは、返されたネイティブエラー番号を適切な SQLSTATE にマップします。 ネイティブエラー番号にマップする ODBC エラーコードがない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC ドライバーは SQLSTATE 42000 ("構文エラーまたはアクセス違反") を返します。 ドライバーによって検出されたエラーについては、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC ドライバーによって適切な SQLSTATE が生成されます。  
  
 状態エラー コードの詳細については、次のトピックを参照してください。  
  
-   [付録 A: ODBC エラー コード](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)  
  
-   [SQLSTATE マッピング](../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
## <a name="see-also"></a>参照  
 [エラーとメッセージの処理](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
