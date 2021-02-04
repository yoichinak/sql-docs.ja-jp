---
description: setAuthenticationScheme (SQLServerDataSource)
title: setAuthenticationScheme (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: b942f78e-7ce1-44ef-923d-a7c3d7c76b83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 93ee3d9cf4769c1552f2c44cedfb21254c046b24
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173956"
---
# <a name="setauthenticationscheme-sqlserverdatasource"></a>setAuthenticationScheme (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  アプリケーションで使用する統合セキュリティの種類を示します。  
  
## <a name="syntax"></a>構文  
  
```vb  
public void setAuthenticationScheme(String authenticationScheme);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *authenticationScheme*  
  
 値は **"JavaKerberos"** であり、既定値は **"NativeAuthentication"** です。 詳細については、「[Kerberos 統合認証による SQL Server への接続](../../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
