---
title: NTLM 認証を使用して SQL Server に接続する
description: JDBC ドライバーで NTLM 認証を使用して SQL データベースの接続を確立する方法について説明します。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: lilgreenbird
ms.author: v-susanh
manager: kenvh
ms.openlocfilehash: ed1e16aac4de3277906d00c2b1a0f4458418cc95
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081771"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>NTLM 認証を使用して SQL Server に接続する

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、アプリケーションで **authenticationScheme** 接続プロパティを使用して、NTLM v2 認証を使用してデータベースに接続することを示すことができます。 

NTLM 認証には、次のプロパティも使用されます。

- **domain = domainName** (省略可能)
- **user = userName**
- **password = password**
- **integratedSecurity = true**

**domain** 以外のプロパティは必須です。**NTLM** authenticationScheme プロパティが使用されている場合、どれかが不足していると、ドライバーによってエラーがスローされます。 

接続プロパティの詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。 Microsoft NTLM 認証プロトコルの詳細については、[Microsoft NTLM](/windows/desktop/SecAuthN/microsoft-ntlm) に関するページを参照してください。

## <a name="remarks"></a>解説

NTLM 認証の動作を制御する、SQL Server 設定の詳細については、[ネットワーク セキュリティ:LAN Manager 認証レベル](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level)に関するページを参照してください。 

## <a name="logging"></a>ログ記録

NTLM 認証をサポートするために、新しいロガー com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication が追加されました。 詳細については、「[ドライバー操作のトレース](../../connect/jdbc/tracing-driver-operation.md)」を参照してください。

## <a name="datasource"></a>DataSource

データソースを使用して接続を作成する場合、NTLM プロパティは、**setAuthenticationScheme**、**setDomain**、および (必要に応じて) **setServerSpn** を使用してプログラムで設定できます。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("NTLM");
ds.setDomain("<domainName>");
ds.setUser("<userName>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setServerSpn("<serverSpn");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

## <a name="service-principal-names"></a>サービス プリンシパル名

サービス プリンシパル名 (SPN) は、クライアントがサービスのインスタンスを一意に識別するための名前です。

**serverSpn** 接続プロパティを使用して SPN を指定できますが、ドライバーで自動的に作成することもできます (既定)。 このプロパティの形式は "MSSQLSvc/fqdn:port\@REALM" です。ここで、fqdn は完全修飾ドメイン名、port はポート番号、REALM は大文字で表記された SQL Server の領域です。 既定の領域がサーバーの領域と同じであるため、このプロパティの領域部分は省略可能です。

たとえば、SPN は次のようになります。"MSSQLSvc/some-server.zzz.corp.contoso.com:1433"

サービス プリンシパル名 (SPN) の詳細については、以下を参照してください。

- [クライアント接続でのサービス プリンシパル名 (SPN) のサポート](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)

> [!NOTE]  
> serverSpn 接続属性は、Microsoft JDBC Driver 4.2 以降でのみサポートされています。

> 6\.2 リリースより前の JDBC driver では、**serverSpn** を明示的に設定する必要があります。 6\.2 リリースの場合、ドライバーは既定で **Serverspn** を構築でき ますが、 **serverspn**を明示的に使用することもできます。

## <a name="security-risks"></a>セキュリティ リスク

NTLM プロトコルは、さまざまな脆弱性を持つ古い認証プロトコルであり、セキュリティ上のリスクがあります。 比較的弱い暗号方式に基づいており、さまざまな攻撃に対して脆弱です。 Kerberos に置き換えられます。これは、より安全で推奨されます。 NTLM 認証は、セキュリティで保護された信頼できる環境、または Kerberos を使用できない場合にのみ使用してください。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、NTLM v2 のみサポートされています。これは、元の v1 プロトコルよりもセキュリティが強化されています。 拡張保護を有効にするか、SSL 暗号化を使用して、セキュリティを強化することもお勧めします。 

拡張保護を有効にする方法の詳細については、以下を参照してください。

- [拡張保護を使用したデータベース エンジンへの接続](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

SSL 暗号化を使用した接続の詳細については、以下を参照してください。

- [SSL 暗号化を使用した接続](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> 7\.4 リリースでは、拡張保護と暗号化の**両方**を有効にすることはサポートされていません。

## <a name="see-also"></a>関連項目

[JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)