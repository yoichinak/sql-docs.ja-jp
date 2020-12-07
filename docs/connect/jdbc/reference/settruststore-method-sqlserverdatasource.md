---
description: setTrustStore メソッド (SQLServerDataSource)
title: setTrustStore メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be69bd333d0264e4833dd053979f1e3dfe5a9b39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354928"
---
# <a name="settruststore-method-sqlserverdatasource"></a>setTrustStore メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  証明書の trustStore ファイルへのパス (ファイル名を含む) を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *trustStore*  
  
 証明書の trustStore ファイルへのパス (ファイル名を含む) を表す **String** です。  
  
## <a name="remarks"></a>解説  
 trustStore プロパティが指定されていないか null に設定されている場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は、信頼マネージャー ファクトリの検索ルールに従って、使用する証明書ストアを決定します。 既定の SunX509 TrustManagerFactory では、次の場所で、この順序に従ってトラスト マテリアルの検索が行われます。  
  
-   1. Java 仮想マシン (JVM) システム プロパティの "javax.net.ssl.trustStore" で指定されたファイル  
  
-   2. "\<java-home>/lib/security/jssecacerts" ファイル。  
  
-   3. "\<java-home>/lib/security/cacerts" ファイル。  
  
 詳細については、Sun Microsystems の Web サイトにある SunX509 TrustManager Interface に関するドキュメントを参照してください。  
  
 trustStore プロパティが文字列または空の文字列 "" に設定されている場合、ドライバーはその値を使用して trustStore ファイルを検索し、サーバーの TLS/SSL 証明書を検証します。  
  
 trustStorePassword プロパティは trustStore プロパティと共に指定でき、その値を trustStore ファイルを開くために使用します。 詳細については、「[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
