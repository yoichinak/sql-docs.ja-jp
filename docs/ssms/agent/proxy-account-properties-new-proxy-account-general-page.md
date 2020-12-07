---
description: '[プロキシ アカウントのプロパティ] - [新しいプロキシ アカウント] ([全般] ページ)'
title: '[プロキシ アカウントのプロパティ] - [新しいプロキシ アカウント] ([全般] ページ)'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a70ba36150771ef90f3cfc9461c018c212da4c73
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037303"
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>[プロキシ アカウントのプロパティ] - [新しいプロキシ アカウント] ([全般] ページ)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントのプロパティを表示したり変更したりできます。  
  
## <a name="options"></a>オプション  
**[プロキシ名]**  
プロキシの名前を入力します。  
  
**[資格情報名]**  
プロキシの資格情報の名前を入力します。  
  
> [!NOTE]  
> 指定する資格情報名は、既存の資格情報の名前である必要があります。 資格情報を作成する方法の詳細については、[プロキシを作成する方法](../../relational-databases/security/authentication-access/create-a-credential.md)に関するページを参照してください  
  
**...**  
**[資格情報の選択]** ダイアログを起動します。  
  
**説明**  
プロキシの説明を入力します。  
  
**[以下のサブシステムに対してアクティブ]**  
プロキシ アカウントがアクセスできるサブシステムを選択します。  
  
**[以下にジョブ ステップを再度割り当てます]**  
ジョブ ステップを再度割り当てるプロキシを選択します。 プロキシが以前アクセスしていたサブシステムに対するアクセスを取り消すときに、この一覧が使用できるようになります。  
  
## <a name="see-also"></a>参照  
[Create a SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
