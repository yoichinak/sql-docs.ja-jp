---
description: setEncrypt メソッド (SQLServerDataSource)
title: setEncrypt メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e7da98aa70be2066c370b75e2bc213c25ba16e03
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431974"
---
# <a name="setencrypt-method-sqlserverdatasource"></a>setEncrypt メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  encrypt プロパティが有効であるかどうかを示す **Boolean** 値が設定されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *encrypt*  
  
 クライアントと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の間で TLS (トランスポート層セキュリティ) (以前の SSL (Secure Sockets Layer)) 暗号化が有効である場合は、**true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>解説  
 encrypt プロパティが **true** に設定されている場合、サーバーに証明書がインストールされていれば、サーバーとクライアント間で送信されるすべてのデータで TLS 暗号化が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で確実に使用されることを [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は保証します。 既定値は **false** です。  
  
 JDBC ドライバーは、TLS ハンドシェイクの確立を試みる際に、使用中の Java 仮想マシン (JVM) を検出します。  
  
 encrypt プロパティが **true** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、JVM の既定の JSSE セキュリティ プロバイダーを使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と TLS 暗号化がネゴシエートされます。 既定のセキュリティ プロバイダーでは、TLS 暗号化の正常なネゴシエートに必要なすべての機能がサポートされているとは限りません。 たとえば、既定のセキュリティ プロバイダーでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の TLS/SSL 証明書で使用されている RSA 公開キーのサイズをサポートしていない場合があります。 この場合、既定のセキュリティ プロバイダーでエラーが発生し、その結果 JDBC ドライバーが接続を終了する可能性があります。 この問題を解決するには、次のいずれかを実行します。  
  
-   サイズの小さい RSA 公開キーを持つサーバー証明書を使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を構成します。  
  
-   "\<java-home>/lib/security/java.security" セキュリティ プロパティ ファイルで、別の JSSE セキュリティ プロバイダーを使用するように JVM を構成します。  
  
-   別の JVM を使用します。  
  
 encrypt プロパティが指定されていないか、または **false** に設定されている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がドライバーによって TLS 暗号化のサポートを強制されることはありません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが TLS 暗号化を強制的に使用するように構成されていない場合、接続は暗号化なしで確立します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが TLS 暗号化を強制的に使用するように構成されている場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、使用中の JVM が適切に構成されていれば、自動的に TLS 暗号化を有効にし、そうでなければ接続を終了しエラーを生成します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
