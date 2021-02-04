---
description: getClientInfoProperties メソッド (SQLServerDatabaseMetaData)
title: getClientInfoProperties メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fe2bb68b8567393ccaa8481e0903bd8b97c5664
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99163334"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>getClientInfoProperties メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ドライバーがサポートしているクライアント情報のプロパティの一覧を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>戻り値  
 ResultSet オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getClientInfoProperties メソッドは、java.sql.DatabaseMetaData インターフェイスの getClientInfoProperties メソッドによって指定されます。  
  
> [!NOTE]  
>  このメソッドでは、空の結果セットが返されます。 ドライバーは **applicationName** の設定のみをサポートし、**applicationName** は接続時にのみ設定されます。 SQL Server では、接続が確立された後のクライアント アプリケーション情報の更新はサポートされていません。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
