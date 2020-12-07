---
description: getObjectInstance メソッド (SQLServerDataSourceObjectFactory)
title: getObjectInstance メソッド (SQLServerDataSourceObjectFactory) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 79510f1e28f6f8933b417ad17ecac34713e885e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435064"
---
# <a name="getobjectinstance-method-sqlserverdatasourceobjectfactory"></a>getObjectInstance メソッド (SQLServerDataSourceObjectFactory)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定したデータ ソース オブジェクトのインスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.Object getObjectInstance(java.lang.Object ref,  
                                          javax.naming.Name name,  
                                          javax.naming.Context c,  
                                          java.util.Hashtable h)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ref*  
  
 **Object** 値。  
  
 *name*  
  
 オブジェクトの名前。  
  
 *c*  
  
 指定した名前に関連するコンテキストです。  
  
 *h*  
  
 オブジェクトの作成に使用する環境です。  
  
## <a name="return-value"></a>戻り値  
 **Object** 値。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>解説  
 この getObjectInstance メソッドは、javax.naming.spi.ObjectFactory インターフェイスの getObjectInstance メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSourceObjectFactory のメソッド](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [SQLServerDataSourceObjectFactory のメンバー](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [SQLServerDataSourceObjectFactory クラス](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
