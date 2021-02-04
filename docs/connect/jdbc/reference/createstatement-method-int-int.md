---
description: createStatement (int, int) メソッド
title: createStatement メソッド (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9adab8077a33fe1856c70c543521dcac3566d200
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168561"
---
# <a name="createstatement-method-int-int"></a>createStatement (int, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された結果セットの種類およびコンカレンシーの [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを生成する [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *resultSetType*  
  
 結果セットの種類を表す **int** 値です。  
  
 *resultSetConcurrency*  
  
 結果セットのコンカレンシーの種類を表す **int** 値です。  
  
## <a name="return-value"></a>戻り値  
 Statement オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この createStatement メソッドは、java.sql.Connection インターフェイスの createStatement メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [createStatement メソッド &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
