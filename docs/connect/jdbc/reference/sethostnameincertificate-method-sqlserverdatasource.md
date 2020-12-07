---
description: setHostNameInCertificate メソッド (SQLServerDataSource)
title: setHostNameInCertificate メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886a32898b04cc8907a832d54a3051222e4d0fb7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431824"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>setHostNameInCertificate メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の TLS (トランスポート層セキュリティ) (以前の SSL (Secure Sockets Layer)) を検証するために使用するホスト名を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *hostNameInCertificate*  
  
 ホスト名を含む**文字列**です。  
  
## <a name="remarks"></a>解説  
 hostNameInCertificate 値は、通信レイヤーが TLS で暗号化されているときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の TLS/SSL 証明書を検証するために使用します。 既定値は、null です。  
  
 hostNameInCertificate プロパティが null に設定されているか、またはそれが指定されていない場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、serverName プロパティ値を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 証明書に対して検証を行います。 hostNameInCertificate プロパティが文字列または空の文字列 "" に設定されている場合、ドライバーはその値を使用してサーバーの TLS/SSL 証明書を検証します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
