---
title: WMI Provider for Configuration Management の使用
description: バインド、接続文字列の指定、アクセス許可/サーバー認証など、構成管理のための WMI プロバイダーについて説明します。
ms.custom: seo-lt-2019
ms.date: 04/12/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2b95e9593493524a0a86579acdd2d96193ea2fb8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542750"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>WMI Provider for Configuration Management の操作

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この記事では、コンピューターの管理のために WMI プロバイダーを使用してプログラミングする方法に関するガイダンスを提供します。

## <a name="binding"></a>バインド  
  WMI Provider for Configuration Management は、COM オブジェクト モデルであり、事前バインドも遅延バインドもサポートしています。 遅延バインドを行う場合、VBScript などのスクリプト言語を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、ネットワーク設定、別名をプログラムで操作することができます。  
  
## <a name="specifying-a-connection-string"></a>接続文字列の指定

アプリケーションは、プロバイダーによって定義された WMI 名前空間に接続することで、WMI Provider for Configuration Management を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにダイレクトします。 Windows WMI サービスは、この名前空間をプロバイダー DLL にマップし、DLL をメモリに読み込みます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスはすべて、1 つの WMI 名前空間で表されます。

名前空間の既定の形式は次のとおりです。 形式では、 `VV` は SQL Server のメジャーバージョン番号です。 この数は、を実行することで検出 `SELECT @@VERSION;` できます。

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

PowerShell を使用して接続する場合は、先頭を `\\.\` 削除する必要があります。 たとえば、次の PowerShell コードは、SQL Server 2016 のすべての WMI クラス (メジャーバージョン 13) を一覧表示します。

```powershell
Get-WmiObject -Namespace 'root\Microsoft\SqlServer\ComputerManagement13' -List
```

<!--
Updated this on 2019-04-12, per:
   ~ https://github.com/MicrosoftDocs/sql-docs/issues/1817
   ~ https://github.com/rrg92/sql-docs/commit/3d518bfc0d55f819c762abc3e5c5c9eed85abe94?diff=unified

Thus from here I (GeneMi = MightyPen) removed the following text about 'instance_name':

'root\Microsoft\SqlServer\ComputerManagement13\instance_name'

where `instance_name` defaults to `MSSQLSERVER` in a default installation of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
-->

次の PowerShell コードを使用して、使用可能なすべての WMI ComputerManagement 名前空間を照会できます。

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **注:** Windows ファイアウォールを介して接続している場合は、コンピューターが適切に構成されていることを確認する必要があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN [Web サイト](https://go.microsoft.com/fwlink/?linkid=15426)の Windows Management Instrumentation のドキュメントで、Windows ファイアウォール経由の接続に関する記事を参照してください。  
  
## <a name="permissions-and-server-authentication"></a>権限とサーバー認証  
 WMI Provider for Configuration Management にアクセスするには、クライアント WMI 管理スクリプトが、ターゲット コンピューター上の管理者のコンテキストで実行されている必要があります。 アクセスするユーザーは、管理するコンピューターのローカル Windows 管理者グループのメンバーである必要があります。  
  
 管理者は、グループ ポリシーを設定して、WMI プロバイダーへのユーザー アクセスを制御することができます。 グループ ポリシーの設定の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーのヘルプの「グループ ポリシーと MMC」を参照してください。  
  
 WMI 管理スクリプトを使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されるアカウントを更新することができます。  
  
 WMI Provider for Configuration Management では、セキュリティ証明書がサポートされています。 証明書の詳細については、「 [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)  
  
  
