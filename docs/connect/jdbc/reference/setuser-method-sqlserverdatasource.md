---
description: setUser メソッド (SQLServerDataSource)
title: setUser メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b887e5b0af5d4a91a8cbea2b3676fd958ac3c077
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472180"
---
# <a name="setuser-method-sqlserverdatasource"></a>setUser メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データ ソースへの接続に使用されるユーザー名を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *user*  
  
 ユーザー名を含む**文字列**です。  
  
## <a name="remarks"></a>解説  
 setUser メソッドでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への接続に使用されるユーザー名が設定されます。 ユーザー名の値が設定されていない場合、[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) メソッドからは既定値の null が返されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
