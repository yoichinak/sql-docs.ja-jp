---
description: setServerName メソッド (SQLServerDataSource)
title: setServerName メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42380a0a3816dd0a3e93472afddc66ffa1ecaa02
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458374"
---
# <a name="setservername-method-sqlserverdatasource"></a>setServerName メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているコンピューターの名前を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *serverName*  
  
 サーバー名を含む**文字列**です。  
  
## <a name="remarks"></a>解説  
 サーバー名は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行している、ターゲット コンピューターのホスト名です。 serverName プロパティが設定されていない場合、[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) は既定値の null が返されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
