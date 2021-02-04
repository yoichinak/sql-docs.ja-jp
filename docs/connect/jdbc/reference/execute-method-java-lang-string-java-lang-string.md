---
description: execute (java.lang.String, java.lang.String) メソッド
title: execute メソッド (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.execute (java.lang.String.java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9451c7c2-4c0d-4d1e-9b42-a26ff28e3f6a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4103e4a10aff5f16c68cfc584d31a1e6600e723
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168477"
---
# <a name="execute-method-javalangstring-javalangstring"></a>execute (java.lang.String, java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  複数の結果を返す可能性のある渡された SQL ステートメントを実行し、渡された配列に示される自動生成キーを検索可能にするように、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] に通知します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final boolean execute(java.lang.String sql,  
                             java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sql*  
  
 SQL ステートメントを含む **文字列** です。  
  
 *columnNames*  
  
 検索可能にする自動生成キーの列名を示す文字列の配列です。  
  
## <a name="return-value"></a>戻り値  
 最初の結果が結果セットの場合は **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この execute メソッドは、java.sql.Statement インターフェイスの execute メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [execute メソッド &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
