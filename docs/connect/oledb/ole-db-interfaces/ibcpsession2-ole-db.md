---
title: IBCPSession2 (OLE DB ドライバー) | Microsoft Docs
description: OLE DB Driver for SQL Server の IBCPSession2 インターフェイスについて説明します。このインターフェイスは、列単位の IBCPSession::BCPColFmt の代わりに使用できる BCPSetBulkMode を提供します。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IBCPSession2 interface
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50cc43cec2e51162a887801bc52dcf34d4df26fa
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862324"
---
# <a name="ibcpsession2-ole-db"></a>IBCPSession2 (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  IBCPSession2 インターフェイスは、IBCPSession の拡張機能です。この機能は、各列に対して IBCPSession::BCPColFmt を呼び出す代わりに使用できるメンバー関数を提供します。  IBCPSession2 は IBCPSession を継承しており、[IBCPSession2::BCPSetBulkMode](../../oledb/ole-db-interfaces/ibcpsession2-bcpsetbulkmode.md) という新しいメソッドが追加されています。  
  
## <a name="see-also"></a>参照  
 [インターフェイス &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
