---
description: setTrustServerCertificate メソッド (SQLServerDataSource)
title: setTrustServerCertificate メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fb76148ae8c63dd30bd1532ec74d545bcc3388d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355098"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>setTrustServerCertificate メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  trustServerCertificate プロパティが有効であるかどうかを示す **Boolean** 値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *trustServerCertificate*  
  
 通信レイヤーが TLS で暗号化されているときに、サーバーの TLS (トランスポート層セキュリティ) (以前の SSL (Secure Sockets Layer)) 証明書が自動的に信頼されるようにする場合は、**true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>解説  
 trustServerCertificate プロパティが **true** に設定されている場合、通信レイヤーが TLS で暗号化されているとき、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の TLS/SSL 証明書は自動的に信頼されます。 つまり、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の TLS/SSL 証明書は検証されません。 既定値は **false** です。  
  
 trustServerCertificate プロパティが **false** に設定されている場合は、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] によってサーバーの TLS/SSL 証明書が検証されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
