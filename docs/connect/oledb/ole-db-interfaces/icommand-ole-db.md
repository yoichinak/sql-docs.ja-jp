---
title: ICommand (OLE DB ドライバー) | Microsoft Docs
description: OLE DB Driver for SQL Server に固有の ICommand::Execute メソッドの動作について説明します。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7d290800b0f002f2ad7ba1703683648a62f41f8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191808"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  この記事では、OLE DB Driver for SQL Server に固有となる OLE DB 動作について説明します。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 列のサイズより大きなデータを挿入すると、通常はエラーが発生します。 しかし、S_OK が返され、`dwStatus` が DBSTATUS_S_TRUNCATED に設定される場合もあります。 この現象が通常発生するシナリオを、次にいくつか示します。

- データをパラメーターで挿入した場合  
- 列のサイズがデータを格納できる十分な大きさでない場合  
- `ICommandWithParameters::SetParameterInfo` が呼び出されていない場合  
  
## <a name="see-also"></a>参照  
 [インターフェイス &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
