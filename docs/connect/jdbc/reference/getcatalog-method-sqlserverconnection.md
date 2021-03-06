---
description: getCatalog メソッド (SQLServerConnection)
title: getCatalog メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aba85b17bade5d9221a22dc98babf0c80b2853ab
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99165548"
---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトの現在のカタログ名を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>戻り値  
 カタログ名を含む **文字列** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getCatalog メソッドは、java.sql.Connection インターフェイスの getCatalog メソッドで指定されています。  
  
 SQLServerConnection オブジェクトの現在のカタログ プロパティを返します。設定されていない場合は null を返します。 カタログ プロパティは、[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) メソッドを使用して明示的に設定されるか、現在のカタログの TDS に対する環境変更を読み取って暗黙的に更新されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
