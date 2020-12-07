---
description: getTrustServerCertificate メソッド (SQLServerDataSource)
title: getTrustServerCertificate メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3a5de057e6a9363f4e3feeace35f2b5105d3cd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434054"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  trustServerCertificate プロパティが有効であるかどうかを示す**ブール**値が返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>戻り値  
 trustServerCertificate が有効な場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>解説  
 trustServerCertificate プロパティが **true** に設定されている場合、通信レイヤーが TLS で暗号化されているときに、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の TLS (トランスポート層セキュリティ) (以前の SSL (Secure Sockets Layer)) 証明書は自動的に信頼されます。 つまり、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の TLS/SSL 証明書は検証されません。 既定値は **false** です。  
  
 trustServerCertificate プロパティが **false** に設定されている場合は、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] によってサーバーの TLS/SSL 証明書が検証されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
