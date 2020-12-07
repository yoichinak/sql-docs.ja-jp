---
description: updateSQLXML (java.lang.String, java.sql.SQLXML) メソッド
title: updateSQLXML (java.lang.String, java.sql.SQLXML) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 60021881-ef83-499b-9977-e20ff23c1312
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80d597d42f17a6a08fc2d9f134f799c38ad04e8a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431224"
---
# <a name="updatesqlxml-method-javalangstring-javasqlsqlxml"></a>updateSQLXML (java.lang.String, java.sql.SQLXML) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を java.sql.SQLXML 値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateSQLXML(java.lang.String columnLabel,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnLabel*  
  
 列ラベルを示す **String** です。  
  
 *xmlObject*  
  
 SQLXML オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateSQLXML メソッドは、java.sql.ResultSet インターフェイスの updateSQLXML メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [updateSQLXML メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
