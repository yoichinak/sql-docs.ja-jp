---
description: getUser メソッド (SQLServerDataSource)
title: getUser メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bd3ac0a7c17d0bd10e8709194c8a13eef7eb25d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99154716"
---
# <a name="getuser-method-sqlserverdatasource"></a>getUser メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データ ソースへの接続に使用されるユーザー名を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>戻り値  
 ユーザー名を含む **文字列** です。  
  
## <a name="remarks"></a>解説  
 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) メソッドでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続するときに使用されるユーザー名が設定されます。 ユーザー名の値が設定されていない場合、getUser メソッドは既定値の null を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
