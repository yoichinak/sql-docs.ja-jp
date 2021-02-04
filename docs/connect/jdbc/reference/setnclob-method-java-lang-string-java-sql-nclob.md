---
description: setNClob (java.lang.String, java.sql.NClob) メソッド
title: setNClob メソッド (java.lang.String, java.sql.NClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 4e30d242-0c1b-45db-b75f-41b041692f31
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 65b425d8c194d2cdb00ed7319e1b5531e871bdc5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173297"
---
# <a name="setnclob-method-javalangstring-javasqlnclob"></a>setNClob (java.lang.String, java.sql.NClob) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、指定された NClob オブジェクトに設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.sql.NClob value)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterName*  
  
 パラメーターの名前を含む **文字列** です。  
  
 *value*  
  
 NClob オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 このメソッドは、**NCHAR**、**NVARCHAR**、**NTEXT**、**XML** の各パラメーター データ型に対して使用する必要があります。  
  
 この setNClob メソッドは、java.sql.CallableStatement インターフェイスの setNClob メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [setNClob メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
