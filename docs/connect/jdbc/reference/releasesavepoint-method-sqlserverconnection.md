---
description: releaseSavepoint メソッド (SQLServerConnection)
title: releaseSavepoint メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.releaseSavepoint
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6b625ea-c7ce-4a32-a9e0-6d2b4321bfd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43a159feee134937fa14889fde196b2115e59494
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174168"
---
# <a name="releasesavepoint-method-sqlserverconnection"></a>releaseSavepoint メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在のトランザクションから、渡された [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) オブジェクトを削除します。  
  
> [!NOTE]  
>  このメソッドは、現在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ではサポートされていません。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void releaseSavepoint(java.sql.Savepoint savepoint)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *savepoint*  
  
 削除する SavePoint オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この releaseSavepoint メソッドは、java.sql.Connection インターフェイスの releaseSavepoint メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
