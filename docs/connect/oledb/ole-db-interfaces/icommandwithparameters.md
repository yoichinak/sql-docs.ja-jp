---
title: ICommandWithParameters (OLE DB ドライバー) | Microsoft Docs
description: OLE DB Driver for SQL Server で期待される結果のより正確な記述を、機能強化により ICommandWithParameters::GetParameterInfo で取得できるようになった方法について説明します。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd33d19aaa5bea8c938ceaafe926b23f256ce703
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191793"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 以降のデータベース エンジンの機能強化により、ICommandWithParameters::GetParameterInfo で、期待される結果のより正確な記述を取得できるようになりました。 結果がより正確になり、以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で CommandWithParameters::GetParameterInfo から返される値とは異なる可能性があります。 詳細については、「[メタデータの検出](../../oledb/features/metadata-discovery.md)」を参照してください。  
  
 また、[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 以降で、ICommandWithParameters::SetParameterInfo を呼び出す際、*pwszName* パラメーターに渡される値は有効な識別子である必要があります。 詳細については、「[データベース識別子](../../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [インターフェイス &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
