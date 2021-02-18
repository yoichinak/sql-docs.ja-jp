---
title: ISSDataClassification | Microsoft Docs
description: ISSDataClassification インターフェイス
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSDataClassification
apitype: COM
helpviewer_keywords:
- ISSDataClassification interface
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 23c575e31f151156165e09c34baf6c81b44b209b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100342482"
---
# <a name="issdataclassification"></a>ISSDataClassification
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../../includes/applies-to-version/sql-asdb-asa.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSDataClassification** インターフェイスにより、SQL Server から受信したアクティブな行セットの秘密度分類データを取得するための機能が提供されます。
  

## <a name="methods"></a>メソッド

|メソッド|説明|  
|------------|-----------------|  
|[ISSDataClassification::GetSensitivityClassification](../../oledb/ole-db-interfaces/issdataclassification-getsensitivityclassification-ole-db.md)|秘密度分類情報を含む SENSITIVITYCLASSIFICATION 構造体へのポインターが返されます。|  

## <a name="see-also"></a>参照  
 [インターフェイス &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [行セット](../ole-db-rowsets/rowsets.md)   
 [データ分類の使用](../features/using-data-classification.md)
