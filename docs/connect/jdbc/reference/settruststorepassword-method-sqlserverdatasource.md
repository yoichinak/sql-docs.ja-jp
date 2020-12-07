---
description: setTrustStorePassword メソッド (SQLServerDataSource)
title: setTrustStorePassword メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustStorePassword Method (SQLServerDataSource)
apilocation:
- setTrustStorePassword Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: fa87cbde-71cc-4f21-bc07-f8ba2b6a0a3f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6ded82d7db8e7dade5c203a348375812b4e04dfc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478629"
---
# <a name="settruststorepassword-method-sqlserverdatasource"></a>setTrustStorePassword メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  trustStore データの整合性を確認するために使用するパスワードを設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setTrustStorePassword(java.lang.String trustStorePassword)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *trustStorePassword*  
  
 trustStore データの整合性を確認するために使用するパスワードを含む **String** です。  
  
## <a name="remarks"></a>解説  
 trustStorePassword プロパティは trustStore プロパティと共に指定でき、その値を trustStore ファイルの整合性を確認するために使用します。  
  
 trustStore プロパティは設定されているが trustStorePassword プロパティは設定されていない場合、trustStore の整合性は確認されません。  
  
 trustStore プロパティと trustStorePassword プロパティの両方が指定されていない場合、ドライバーでは、Java 仮想マシン (JVM) システム プロパティの "javax.net.ssl.trustStore" と "javax.net.ssl.trustStorePassword" が使用されます。 "javax.net.ssl.trustStorePassword" システム プロパティが指定されていない場合、trustStore の整合性は確認されません。  
  
 trustStore プロパティは設定されていないが trustStorePassword プロパティは設定されている場合、JDBC ドライバーでは、"javax.net.ssl.trustStore" で指定されたファイルがトラスト ストアとして使用され、指定された trustStorePassword を使用してトラスト ストアの整合性が確認されます。 これは、クライアント アプリケーションでパスワードを JVM システム プロパティに格納しないようにする場合に必要となることがあります。  
  
 詳細については、「[接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。  
  
 JDBC Driver 3.0 以降では、SQLServerDataSource.setTrustStorePassword を設定してから、データ ソースのプロパティをバインドする場合は、SQLServerDataSource.setTrustStorePassword を呼び出してから接続を取得する必要があります。 詳細については、「[SQLServerDataSource.getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
