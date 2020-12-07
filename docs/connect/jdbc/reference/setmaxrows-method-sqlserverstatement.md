---
description: setMaxRows メソッド (SQLServerStatement)
title: setMaxRows メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ec693120859dc49d162252f9b0ec768d69365e0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725433"
---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  任意の [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトが含むことのできる最大行数の制限が、渡された数値に設定されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *max*  
  
 最大行数を示す **int** です。制限しない場合は 0 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setMaxRows メソッドは、java.sql.Statement インターフェイスの setMaxRows メソッドによって指定されます。  
  
 この setMaxRows メソッドは、スクロール可能な動的カーソルには影響しません。 大きな結果セットから行が返される可能性がある場合に、返される行数を制限するには、アプリケーションで SELECT TOP N SQL 構文を使用してください。  
  
 setMaxRows メソッドが呼び出されると、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ではアプリケーションのクエリの実行時に SET ROWCOUNT SQL ステートメントが実行されます。 これにより、そのクエリによって返される行の数だけでなく、そのクエリで実行されるすべての [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントによって影響を受ける行の最大数も JDBC ドライバーによって制限されます。 アプリケーションで最上位の [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトに対してのみ制限を設定する必要がある場合は、setMaxRows メソッドではなく、SELECT TOP N SQL 構文をクエリで使用してください。  
  
 SET ROWCOUNT SQL ステートメントの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「[SET ROWCOUNT (Transact-SQL)](../../../t-sql/statements/set-rowcount-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
