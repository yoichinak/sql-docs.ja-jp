---
description: SQL Server エージェントのセキュリティの実装
title: SQL Server エージェントのセキュリティの実装
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 45c136d29261b2ba4ce12185a7a9e437147f990b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037935"
---
# <a name="implement-sql-server-agent-security"></a>SQL Server エージェントのセキュリティの実装
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用すると、データベース管理者は、各ジョブ ステップをそのジョブ ステップの実行に必要な権限だけがあるセキュリティ コンテキスト内で実行できます。適切なセキュリティ コンテキストは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシによって決まります。 特定のジョブ ステップに対応する権限を設定するには、必要な権限のあるプロキシを作成し、そのプロキシをジョブ ステップに割り当てます。 プロキシは、複数のジョブ ステップに対して指定できます。 同じ権限を必要とするジョブ ステップに対しては、同じプロキシを使用します。  
  
次のセクションでは、ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用してジョブを作成または実行するために、許可する必要のあるデータベース ロールについて説明します。  
  
## <a name="granting-access-to-sql-server-agent"></a>SQL Server エージェントへのアクセスの許可  
ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用するには、次の 1 つ以上の固定データベース ロールのメンバーである必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
上記のロールは、 **msdb** データベースに格納されています。 既定では、これらのデータベース ロールのメンバーであるユーザーはいません。 これらのロールのメンバーシップは、明示的に許可する必要があります。 **sysadmin** 固定サーバー ロールのメンバーであるユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントへのフル アクセスが許可されているので、上記の固定データベース ロールのメンバーでなくても [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用できます。 上記のいずれかのデータベース ロールまたは **sysadmin** ロールのメンバーでないユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する際に、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]エージェント ノードを使用できません。  
  
これらのデータベース ロールのメンバーは、自身が所有するジョブの表示および実行に加えて、既存のプロキシ アカウントとして実行するジョブ ステップの作成を行えます。 これらの各ロールに関連付けられている特定の権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
**sysadmin** 固定サーバー ロールのメンバーには、プロキシ アカウントを作成、変更、および削除する権限があります。 **sysadmin** ロールのメンバーには、プロキシを指定せずに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントとして実行するジョブ ステップを作成する権限があります。このアカウントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの起動に使用されるアカウントです。  
  
## <a name="guidelines"></a>ガイドライン  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのセキュリティを向上するには、次のガイドラインに従ってください。  
  
-   プロキシ専用のユーザー アカウントを作成し、ジョブ ステップの実行にはこれらのプロキシ ユーザー アカウントのみを使用します。  
  
-   プロキシ ユーザー アカウントに対し、必要な権限のみを許可します。 特定のプロキシ アカウントに割り当てられたジョブ ステップの実行に実際に求められる権限だけを許可してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスは、Windows **Administrators** グループのメンバーである Microsoft Windows アカウントで実行しないでください。  
  
-   プロキシの安全性は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資格情報ストアと同程度です。  
  
-   ユーザーの書き込み操作で NT イベント ログへの書き込みが可能な場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを介して警告を発行できます。  
  
-   NT Admin アカントを、サービス アカウントまたはプロキシ アカウントとして指定しないでください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、他方の資産にアクセスできます。 この 2 つのサービスは単一の処理領域を共有し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの sysadmin になります。  
  
-   TSX が MSX で参加する場合、MSX の sysadmin が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の TSX インスタンスを完全に制御します。  
  
-   ACE は拡張機能であり、それ自体を呼び出すことはできません。 ACE は Chainer ScenarioEngine.exe (別名 Microsoft.SqlServer.Chainer.Setup.exe) によって呼び出されるか、別のホスト プロセスによって呼び出すことができます。  
  
-   ACE は、SSDP によって所有される次の構成 DLL に依存します。理由は、これらの DLL の API は ACE によって呼び出されるためです。  
  
    -   **SCO**: Microsoft.SqlServer.Configuration.Sco.dll。仮想アカウント用の新しい SCO 検証が含まれます。  
  
    -   **Cluster**: Microsoft.SqlServer.Configuration.Cluster.dll  
  
    -   **SFC**: Microsoft.SqlServer.Configuration.SqlConfigBase.dll  
  
    -   **Extension**: Microsoft.SqlServer.Configuration.ConfigExtension.dll  
  
## <a name="see-also"></a>参照  
[定義済みロールの使用](../../reporting-services/security/role-definitions-predefined-roles.md)  
[sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
[sp_droprolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)  
[セキュリティと保護 (データベース エンジン)](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
