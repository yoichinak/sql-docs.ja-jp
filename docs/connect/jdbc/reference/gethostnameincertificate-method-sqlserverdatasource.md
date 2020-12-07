---
description: getHostNameInCertificate メソッド (SQLServerDataSource)
title: getHostNameInCertificate メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26e931b104c1eba44a09e1b43b51e00d2beaad70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435874"
---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>getHostNameInCertificate メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQL Server の TLS (トランスポート層セキュリティ) (以前の SSL (Secure Sockets Layer)) 証明書を検証するために使用するホスト名が返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>戻り値  
 ホスト名を含む **String** です。値が設定されていない場合は null です。  
  
## <a name="remarks"></a>解説  
 ホスト名は、通信レイヤーが TLS/SSL で暗号化されているときに、SQL Server の TLS/SSL 証明書の値を検証するために使用されます。  
  
 ホスト名が設定されていない場合、[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) メソッドは null を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
