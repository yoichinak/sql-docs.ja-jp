---
title: Azure SQL Database への接続
description: この記事では、Microsoft JDBC Driver for SQL Server を使用して Azure SQL データベースに接続する際の問題について説明します。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bda9c33588c8248d0aff62f555ec46451d0e9e78
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725493"
---
# <a name="connecting-to-an-azure-sql-database"></a>Azure SQL Database への接続

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事では、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用して [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] に接続する際の問題について説明します。 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] への接続に関する詳細については、次をご覧ください。  
  
- [Azure SQL Database](/azure/sql-database/sql-database-technical-overview)  
  
- [方法: JDBC を使用して Azure SQL に接続する](/azure/sql-database/sql-database-connect-query-java)  

- [Azure Active Directory 認証を利用した接続](connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>詳細

[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] に接続する際には、master データベースに接続して **SQLServerDatabaseMetaData.getCatalogs** を呼び出す必要があります。  
[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] では、ユーザー データベースからカタログ全体を返すことがサポートされていません。 **SQLServerDatabaseMetaData.getCatalogs** は sys.databases ビューを使用してカタログを取得します。 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] での **SQLServerDatabaseMetaData.getCatalogs** の動作を 理解するには、[sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) の権限に関する説明を参照してください。  
  
## <a name="connections-dropped"></a>接続のドロップ

[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] への接続時に非アクティブな状態が一定時間続くと、ネットワーク コンポーネント (ファイアウォールなど) によってアイドル接続が終了されることがあります。 このコンテキストでのアイドル接続には、次の 2 種類があります。  

- TCP レイヤーでのアイドル状態。これは、任意の数のネットワーク デバイスによる切断が可能である状態です。  

- Azure SQL ゲートウェイによるアイドル状態。これは、TCP **keepalive** メッセージ (TCP から見て接続がアイドルでない状態にするため) が発生することはあっても、アクティブなクエリが 30 分間発生していないという状態です。 この場合ゲートウェイは、TDS 接続が 30 分間アイドル状態であると判断し、接続を終了します。  
  
ネットワーク コンポーネントによってアイドル接続がドロップされる状況を回避するには、ドライバーが読み込まれているオペレーティング システムで、次のレジストリ設定 (Windows 以外の場合はこれらに相当する設定) を行う必要があります。  
  
|レジストリ設定|推奨値|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ TcpMaxDataRetransmissions|10|  
  
設定後にコンピューターを再起動して、レジストリ設定を有効にします。  

Azure で実行している場合にこれを行うには、スタートアップ タスクを作成してこれらのレジストリ キーを追加します。  たとえば、次のスタートアップ タスクをサービス定義ファイルに追加します。  

```xml
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```

次に、AddKeepAlive.cmd ファイルをプロジェクトに追加します。 [出力ディレクトリにコピー] を [常にコピーする] に設定します。 AddKeepAlive.cmd ファイルのサンプルを次に示します。  

```bat
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on Azure SQL  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```

## <a name="appending-the-server-name-to-the-userid-in-the-connection-string"></a>接続文字列内の userId へのサーバー名の追加  

Version 4.0 より前の [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] に接続する際に、接続文字列内の UserId にサーバー名を追加する必要がありました。 たとえば、「 user@servername 」のように入力します。 Version 4.0 以降の [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、接続文字列内の UserId に @servername を追加する必要がなくなりました。  

## <a name="using-encryption-requires-setting-hostnameincertificate"></a>暗号化の使用に必要な hostNameInCertificate の設定

バージョン 7.2 より前の [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、**encrypt=true** を指定した場合、[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] に接続する際に **hostNameInCertificate** を指定する必要がありました (接続文字列のサーバー名が *shortName*.*domainName* の場合、**hostNameInCertificate** プロパティを \*.*domainName* に設定します)。 バージョン 7.2 以降のドライバーでは、このプロパティは省略可能です。

次に例を示します。

```java
jdbc:sqlserver://abcd.int.mscds.com;databaseName=myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate=*.int.mscds.com;
```

## <a name="see-also"></a>関連項目

[JDBC ドライバーによる SQL Server への接続](connecting-to-sql-server-with-the-jdbc-driver.md)