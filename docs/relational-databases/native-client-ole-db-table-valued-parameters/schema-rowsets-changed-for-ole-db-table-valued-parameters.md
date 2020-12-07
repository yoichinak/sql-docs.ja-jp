---
description: SQL Server Native Client で OLE DB テーブル値パラメーターのスキーマ行セットが変更されました
title: スキーマ行セット、OLE DB テーブル値パラメーター
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d68366d87fdee64096ebca492b318c711fd2b038
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482608"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters-in-sql-server-native-client"></a>SQL Server Native Client で OLE DB テーブル値パラメーターのスキーマ行セットが変更されました
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  テーブル値パラメーターをサポートするために変更または追加されたスキーマ行セットは次のとおりです。  
  
|スキーマ行セット|説明|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|SS_TYPE_CATALOG_NAME および SS_TYPE_SCHEMANAME という名前の 2 つの新しい列が、行セットの末尾に追加されました。 これらの列は、今後の型に再利用できます。 TYPE_NAME 列および LOCAL_TYPE_NAME 列には、テーブル値パラメーター TABLE 型の名前が含まれます。 DATA_TYPE 列には、テーブル値パラメーターの値 DBTYPE_TABLE = 143 が含まれます。|  
|DBSCHEMA_TABLE_TYPES|この行セットは、テーブル値パラメーターをサポートするために追加されました。 これは、DBSCHEMA_TABLES と似ていますが、テーブル、ビュー、またはシノニムではなく、テーブル型のメタデータのみを返す点が異なります。 TABLE_TYPE 列の値は、'TABLE TYPE' になります。|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|この行セットは、テーブル値パラメーターをサポートするために追加されました。 これは、DBSCHEMA_PRIMARY_KEYS と似ていますが、テーブルではなく、テーブル型の主キーのメタデータのみを返す点が異なります。|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|この行セットは、テーブル値パラメーターをサポートするために追加されました。 これは、DBSCHEMA_COLUMNS と似ていますが、テーブル、ビュー、またはシノニムではなく、テーブル型の列のメタデータのみを返す点が異なります。|  
|||

## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
