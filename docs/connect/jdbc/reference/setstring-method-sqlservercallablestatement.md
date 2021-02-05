---
description: setString メソッド (SQLServerCallableStatement)
title: setString メソッド (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerCallableStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f38b97b5-d4f0-4f74-a33d-740241a85842
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24334ffd36b51017b5b46e3aebebe52a7d913b0f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178579"
---
# <a name="setstring-method-sqlservercallablestatement"></a>setString メソッド (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、渡された Java **String** 値に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setString(java.lang.String sCol,  
                      java.lang.String s)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sCol*  
  
 パラメーターの名前を表す **文字列** です。  
  
 *s*  
  
 **文字列** 値です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setString メソッドは、java.sql.CallableStatement インターフェイスの setString メソッドで規定されています。  
  
 文字列からバイナリへの変換を実行できるのは、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] で変換先の型がバイナリであることが認識されている場合のみです。 JDBC ドライバーで基になる型が認識されていない場合、JDBC ドライバーは **String** リテラルを渡し、サーバーで変換を実行できないときは、サーバー エラーを返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
