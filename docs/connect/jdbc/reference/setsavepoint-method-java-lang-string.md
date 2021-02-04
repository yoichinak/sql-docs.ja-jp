---
description: setSavepoint (java.lang.String) メソッド
title: setSavepoint メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4de9512d95c3652dab96bc78fc501e8441afbeb8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173152"
---
# <a name="setsavepoint-method-javalangstring"></a>setSavepoint (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された名前を持つセーブポイントを現在のトランザクションに作成し、そのセーブポイントを表す新しい [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) オブジェクトを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.Savepoint setSavepoint(java.lang.String sName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sName*  
  
 セーブポイントの名前を含む **文字列** 値です。  
  
## <a name="return-value"></a>戻り値  
 SavePoint オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setSavePoint メソッドは、java.sql.Connection インターフェイスの setSavePoint メソッドによって指定されます。  
  
 *sName* 引数は、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] によって自動的にエスケープされます。  
  
## <a name="see-also"></a>参照  
 [setSavepoint メソッド &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
