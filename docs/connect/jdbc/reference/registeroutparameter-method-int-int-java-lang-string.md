---
description: registerOutParamete (int, int, java.lang.String) メソッド
title: registerOutParameter メソッド (int, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3eb5c384-6751-4d50-be23-0c2ccc35593c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dbd25a410a25923e0d13acde8fa52f4061ec0deb
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174238"
---
# <a name="registeroutparameter-method-int-int-javalangstring"></a>registerOutParamete (int, int, java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された順番の位置にある OUT パラメーターを、渡された JDBC 型と型名に登録します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 java.lang.String typeName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *インデックス*  
  
 パラメーターの位置を表す序数を示す **int** です。  
  
 *sqlType*  
  
 java.sql.Types で定義されている JDBC 型コード。  
  
 *typeName*  
  
 完全修飾 SQL 型名を含む **文字列** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この registerOutParameter メソッドは、java.sql.CallableStatement インターフェイスの registerOutParameter メソッドによって指定されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 以降、*sqlType* が java.sql.Types.TIME 型の場合、このメソッドの動作は、**sendTimeAsDatetime** 接続プロパティ (「[接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)」) および [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) によって変更されます。  
  
 詳細については、「[java.sql.Time の値をサーバーに送信する方法の構成](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [registerOutParameter メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
