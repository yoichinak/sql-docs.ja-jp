---
description: setURL メソッド (SQLServerCallableStatement)
title: setURL メソッド (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerCallableStatement.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d83675e-74ca-49d9-8461-6326773c5c8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21cc042fdf2e71000c08fe4085353b080c683256
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99172923"
---
# <a name="seturl-method-sqlservercallablestatement"></a>setURL メソッド (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、渡された URL 値に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setURL(java.lang.String sCol,  
                   java.net.URL u)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sCol*  
  
 パラメーターの名前を表す **文字列** です。  
  
 *u*  
  
 URL オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setURL メソッドは、java.sql.CallableStatement インターフェイスの setURL メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
