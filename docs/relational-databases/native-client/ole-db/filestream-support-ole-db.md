---
description: FILESTREAM のサポート (OLE DB)
title: FILESTREAM のサポート (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8dd62a70c60ff1242aa4ea8b81c85e9ae6046ea1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428074"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM のサポート (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 以降では、OLE DB では、拡張された FILESTREAM 機能がサポートされています。 この機能の詳細については、「 [FILESTREAM のサポート](../../../relational-databases/native-client/features/filestream-support.md)」を参照してください。 サンプルについては、「[FILESTREAM と OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)」を参照してください。  
  
 アプリケーションで 2 GB より大きい **varbinary(max)** 値を送受信するには、パラメーターと結果のバインドで **DBTYPE_IUNKNOWN** を使用します。 パラメーターの場合、プロバイダーは ISequentialStream および ISequentialStream を返す結果に対して IUnknown::QueryInterface を呼び出す必要があります。  
  
 OLE DB の場合は、ISequentialStream 値に関連するチェックが緩和されます。 *wType* が **DBBINDING** 構造体内で **DBTYPE_IUNKNOWN** である場合、*dwPart* から **DBPART_LENGTH** を省略するか、データの長さ (データ バッファー内のオフセット *obLength*) を ~0 に設定することにより、長さのチェックを無効にすることができます。 この場合、プロバイダーは値の長さをチェックせず、ストリームで利用可能なすべてのデータを要求し、返します。 この変更は、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (以降の) サーバーに接続する場合に限り、すべてのラージ オブジェクト (LOB) 型と XML に適用されます。 これにより、既存のアプリケーションや下位レベルのサーバーとの一貫性や下位互換性を維持しつつ、より柔軟な開発が可能になります。  
  
 この変更は、データを転送するすべてのインターフェイス (主に IRowset:: GetData、ICommand:: Execute、および IRowsetFastLoad::InsertRow) に影響します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
