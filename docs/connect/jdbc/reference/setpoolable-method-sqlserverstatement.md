---
description: setPoolable メソッド (SQLServerStatement)
title: setPoolable メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: f0f798c8-cafb-4acc-b85d-2e0059c91d92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d2ae78a9cfeaf4f6391f5c9e74899c90ff50203f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178712"
---
# <a name="setpoolable-method-sqlserverstatement"></a>setPoolable メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ステートメントをプールすること、またはプールしないことを要求します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setPoolable(boolean poolable) throws SQLException  
```  
  
#### <a name="parameters"></a>パラメーター  
 *poolable*  
  
 **true** の場合、ステートメントをプールすることを要求します。 **false** の場合、ステートメントをプールしないことを要求します。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 *poolable* パラメーターに指定する値は、アプリケーションでステートメントをプールする必要があるかどうかをステートメント プールの実装に示すヒントです。 そのヒントを使用するかどうかは、ステートメント プール マネージャーによって決定されます。  
  
 ステートメントのプール値は、ドライバーによって実装される内部ステートメント キャッシュと、アプリケーション サーバーや他のアプリケーションによって実装される外部ステートメント キャッシュの両方に適用されます。  
  
 既定では、SQLServerStatement オブジェクトは作成時にプールできません。 SQLServerPreparedStatement オブジェクトと SQLServerCallableStatement オブジェクトは、作成時にプールできます。  
  
 このメソッドを閉じたステートメントで呼び出すと、[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) がスローされます。  
  
 [isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md) は、オブジェクトをプールできるかどうかを示す値を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
