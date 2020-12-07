---
description: SQLParamData
title: SQLParamData |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: af2f9651ad0bc8986df1c688e4d94084ddeac0df
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810928"
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SQLParamData が、テーブル値パラメーターに関連付けられた *Valueptrptr* を返す場合、アプリケーションは *StrLen_Or_Ind*を使用して sqlparamdata を呼び出す必要があります。 *StrLen_Or_Ind*の値が0より大きい場合は、アプリケーションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 次のテーブル値パラメーター行のパラメーターデータを収集する準備ができていることを意味します。 *StrLen_Or_Ind*の値が0の場合は、テーブル値パラメーターのデータ行がこれ以上存在しないことを意味します。 詳細については、「 [テーブル値パラメーターと列値のバインドとデータ転送](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)」を参照してください。  
  
 テーブル値パラメーターの詳細については、「 [テーブル値パラメーター &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLParamData](../../odbc/reference/syntax/sqlparamdata-function.md)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
