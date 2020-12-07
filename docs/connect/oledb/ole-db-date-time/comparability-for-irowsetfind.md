---
title: IRowsetFind での比較 | Microsoft Docs
description: OLE DB Driver for SQL Server で日付/時刻型に対して IRowsetFind がサポートする比較について説明します。 その他の比較については、DB_E_BADCOMPAREOP が返されます。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16ef589a18c2be5317157e7db5790af06c8c613a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861403"
---
# <a name="comparability-for-irowsetfind"></a>IRowsetFind での比較
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  日付型または時刻型の場合のみ、IRowsetFind では、次の比較がサポートされます。  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 その他の比較を試みると、DB_E_BADCOMPAREOP が返されます。 これは OLE DB 仕様に従っています。  
  
## <a name="see-also"></a>参照  
 [日付と時刻の強化機能 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
