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
ms.openlocfilehash: bf787628804f3597fa724c0ab6313a450e365d58
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861898"
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
  
  
