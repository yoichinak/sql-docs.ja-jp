---
description: setFailoverPartner メソッド (SQLServerDataSource)
title: setFailoverPartner メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c47da87d002d67f98cf80f4cd5db19510c744a03
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178982"
---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>setFailoverPartner メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベース ミラーリング構成で使用されるフェールオーバー サーバーの名前を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *serverName*  
  
 フェールオーバー サーバー名を含む **String** です。  
  
## <a name="remarks"></a>解説  
 このメソッドで設定された値は、プリンシパル サーバーへの初期接続に失敗した場合に使用されます。初期接続が行われた後は、この値は無視されます。 [setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md) メソッドは、このメソッドと共に使用する必要があります。そうしなければ例外がスローされます。  
  
 フェールオーバー サーバーの名前を設定する場合、ドライバーではフェールオーバー サーバーのポート番号を指定することはできません。 ただし、[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) メソッドで [setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md) メソッドおよび [setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md) メソッドを呼び出すことはできます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
