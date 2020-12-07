---
description: SQLServerCallableStatement クラス
title: SQLServerCallableStatement クラス | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a43f718b3a4723710246b85bc166bb52d24a3f8f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355088"
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  入力パラメーターおよび出力パラメーターと共に、呼び出すストアド プロシージャの名前を指定できます。 また、`? = call( ?, ..)` 構文を使用して状態の戻り値を取得することもできます。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **実装:** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **継承:** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>解説  
 SQLServerCallableStatement を使用すると、呼び出すストアド プロシージャの名前と共に、入力および出力パラメーターを指定できます。 また、SQLServerCallableStatement では `? = call( ?, ..)` 構文を使用して状態の戻り値を取得することもできます。  
  
 このクラスでは、SQLServerCallableStatement クラス、ISQLServerCallableStatement インターフェイス、java.sql.CallableStatement インターフェイス、および SQLServerPreparedStatement によってラップ解除がサポートされているクラスとインターフェイスへのラップ解除がサポートされます。 詳細については、「[ラッパーとインターフェイス](../../../connect/jdbc/wrappers-and-interfaces.md)」を参照してください。  
  
 SQLServerCallableStatement のいずれかの set メソッドを特定の型に対して呼び出すとき、その型が、[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) によって指定された型と競合する場合、最後の SQLServerCallableStatement の set メソッドによって指定された型が使用されます。 ただし、その結果、データ型の非互換性から変換エラーが発生する可能性があります。 SQLServerCallableStatement の set メソッドが呼び出されなかった場合、最初の [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 呼び出しで指定された型が使用されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 は、結果セットと更新数が OUT パラメーターよりも先に取得されなければならないという JDBC 4.0 の勧告に準拠しています。 結果セットと更新数が完全に処理される前に OUT パラメーターが取得された場合、処理の済んでいない結果セットと更新数はすべて失われます。  
  
## <a name="see-also"></a>参照  
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
