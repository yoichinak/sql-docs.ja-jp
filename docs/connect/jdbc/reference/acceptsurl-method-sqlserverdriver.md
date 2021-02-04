---
description: acceptsURL メソッド (SQLServerDriver)
title: acceptsURL メソッド (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDriver.acceptsURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fc744566-7191-4b15-9f76-b4b8087fb14a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0269ab57fb0be55f57c8fb97c5d39f6cda37359e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168752"
---
# <a name="acceptsurl-method-sqlserverdriver"></a>acceptsURL メソッド (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された URL が有効であるかどうかを確認します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean acceptsURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *url*  
  
 データベースへの接続に使用される URL を含む **String** 値です。  
  
## <a name="return-value"></a>戻り値  
 渡された URL が有効である場合は **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この acceptsURL メソッドは、java.sql.Driver インターフェイスの acceptsURL メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDriver のメソッド](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver のメンバー](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver クラス](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
