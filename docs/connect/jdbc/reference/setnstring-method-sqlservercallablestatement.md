---
description: setNString メソッド (SQLServerCallableStatement)
title: setNString メソッド (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 6494300b-7fc0-4076-8311-22d35a96cdc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8dfac38c928e939f4d5c3fa29f561c086fefc4d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173276"
---
# <a name="setnstring-method-sqlservercallablestatement"></a>setNString メソッド (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、指定された String オブジェクトに設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setNString(java.lang.String parameterName, java.lang.String value)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterName*  
  
 パラメーターの名前を示す **String** です。  
  
 *value*  
  
 String オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 このメソッドは、**NCHAR**、**NVARCHAR**、**NTEXT**、**XML** の各データ型に対して使用する必要があります。  
  
 この setNString メソッドは、java.sql.CallableStatement インターフェイスの setNString メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
