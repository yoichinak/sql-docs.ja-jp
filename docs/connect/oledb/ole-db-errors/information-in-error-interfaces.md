---
title: エラー インターフェイス内の情報
description: OLE DB Driver for SQL Server では、OLE DB 定義のエラー インターフェイス IErrorInfo、IErrorRecords、ISQLErrorInfo によって、一部のエラーと状態情報が報告されます。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7651d01bef5b17981c0e4c93c450f26e7970524d
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081921"
---
# <a name="information-in-error-interfaces"></a>エラー インターフェイス内の情報
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server は、OLE DB 定義のエラー インターフェイス **IErrorInfo**、**IErrorRecords**、および **ISQLErrorInfo** によって、一部のエラーと状態情報を報告します。  
  
 OLE DB Driver for SQL Server では、次の **IErrorInfo** メンバー関数がサポートされています。  
  
|メンバー関数|説明|  
|---------------------|-----------------|  
|**GetDescription**|エラー メッセージを説明する文字列を返します。|  
|**GetGUID**|エラーを定義したインターフェイスの GUID を返します。|  
|**GetHelpContext**|サポートされていません。 常にゼロが返されます。|  
|**GetHelpFile**|サポートされていません。 常に NULL が返されます。|  
|**GetSource**|文字列 "Microsoft OLE DB Driver for SQL Server"。|  
  
 OLE DB Driver for SQL Server では、コンシューマーが使用できる、次の **IErrorRecords** メンバー関数がサポートされています。  
  
|メンバー関数|説明|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|エラーに関する基本情報を ERRORINFO 構造体に設定します。 ERRORINFO 構造体には、エラーの HRESULT 戻り値およびエラーが適用されるプロバイダーとインターフェイスを特定するメンバーが含まれます。|  
|**GetCustomErrorObject**|**ISQLErrorInfo** インターフェイスと [ISQLServerErrorInfo](../ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md) インターフェイスの参照を返します。|  
|**GetErrorInfo**|**IErrorInfo** インターフェイスの参照を返します。|  
|**GetErrorParameters**|OLE DB Driver for SQL Server では、**GetErrorParameters** 経由でコンシューマーにパラメーターを返すことはありません。|  
|**GetRecordCount**|使用できるエラー レコードの数を返します。|  
  
 OLE DB Driver for SQL Server では、次の **ISQLErrorInfo::GetSQLInfo** パラメーターがサポートされています。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*pbstrSQLState*|エラーの SQLSTATE 値を返します。 SQLSTATE 値は、SQL-92、ODBC と ISO SQL、および API の各仕様で定義されています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] または OLE DB Driver for SQL Server でも、実装固有の SQLSTATE 値は定義されません。|  
|*plNativeError*|該当する場合は、**master.dbo.sysmessages** から [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のエラー番号を返します。 OLE DB Driver for SQL Server のデータ ソースの初期化の試行が成功すると、ネイティブ エラーが使用できるようになります。 この試行の前は、OLE DB Driver for SQL Server では常に 0 が返されます。|  
  
## <a name="see-also"></a>参照  
 [エラー](../../oledb/ole-db-errors/errors.md)  
  
