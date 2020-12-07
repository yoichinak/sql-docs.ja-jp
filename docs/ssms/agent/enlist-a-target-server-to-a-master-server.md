---
description: マスター サーバーへのターゲット サーバーの参加
title: マスター サーバーへのターゲット サーバーの参加
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a936e1a601401787a36470d3119897ec0c5c5b77
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038886"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>マスター サーバーへのターゲット サーバーの参加
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このトピックでは、マルチサーバー管理構成にターゲット サーバーを参加させる方法について説明します。 この手順はマスター サーバーから実行します。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、または SQL Server 管理オブジェクト (SMO) を使用します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス用に使用される Windows アカウントがマルチサーバー環境に与える影響については、「 [マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)」を参照してください。  
  
マスター サーバーとターゲット サーバー間の接続では、既定で完全なトランスポート層セキュリティ (TLS) (旧称 Secure Sockets Layer (SSL)) の暗号化と証明書の検証が有効です。 詳しくは、「[ターゲット サーバーでの暗号化オプションの設定](../../ssms/agent/set-encryption-options-on-target-servers.md)」をご覧ください。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-enlist-a-target-server"></a>ターゲット サーバーを参加させるには  
  
1.  **オブジェクト エクスプローラー**で、マスター サーバーとして構成するサーバーを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチ サーバーの管理]** をポイントして **[ターゲット サーバーの追加]** をクリックします。  
  
3.  ターゲット サーバー設定ウィザードを実行し、指示に従って操作します。  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-enlist-a-target-server"></a>ターゲット サーバーを参加させるには  
  
1.  **sp_msx_enlist** ストアド プロシージャを使用します。  詳細については、「 [sp_msx_enlist (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
