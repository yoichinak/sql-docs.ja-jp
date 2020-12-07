---
title: SQL Server での認証
description: ADO.NET の使用時の SQL Server のログインと認証、および追加リソースの検索場所について説明します。
ms.date: 09/26/2019
dev_langs:
- csharp
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 8bdcc51fad2bbc14499b60a1986bec5d2bcb6a1e
ms.sourcegitcommit: 2600a414c321cfd6dc6daf5b9bcbc9a99c049dc4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603488"
---
# <a name="authentication-in-sql-server"></a>SQL Server での認証

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server は、Windows 認証モードと混合モードという 2 つの認証モードをサポートしています。  
  
- Windows 認証は既定の認証モードです。この SQL Server セキュリティ モデルは Windows と緊密に統合されているため、多くの場合、統合セキュリティと呼ばれます。 特定の Windows ユーザー アカウントとグループ アカウントは、SQL Server へのログインが信頼されています。 すでに認証されている Windows ユーザーは、追加の資格情報を提示する必要はありません。  
  
- 混合モードは、Windows による認証と SQL Server による認証の両方がサポートされます。 ユーザー名とパスワードの組み合わせは、SQL Server 内で管理されます。  
  
> [!IMPORTANT]
> 可能な限り、Windows 認証を使用することが推奨されます。 Windows 認証では、暗号化された一連のメッセージを使用して SQL Server のユーザーを認証します。 SQL Server ログインを使用した場合、SQL Server のログイン名と暗号化されたパスワードがネットワーク経由で渡されるためセキュリティが低下します。  
  
Windows 認証では、既に Windows にログオンしているユーザーが別途 SQL Server にログオンする必要はありません。 次の `SqlConnection.ConnectionString` では Windows 認証が指定されるため、ユーザー名もパスワードもユーザーに要求させません。  
  
```csharp
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
> ログインはデータベース ユーザーとは異なります。 ログインまたは Windows グループは、別の操作でデータベース ユーザーまたはロールにマップする必要があります。 次に、データベース オブジェクトにアクセスするためのアクセス許可をユーザーまたはロールに付与します。  
  
## <a name="authentication-scenarios"></a>認証シナリオ  
Windows 認証は通常、次の状況に最適な選択肢です。  
  
- ドメイン コントローラーがある。  
  
- アプリケーションとデータベースが同じコンピューター上にある。  
  
- SQL Server Express または LocalDB のインスタンスを使用している。  
  
SQL Server のログインは、次の状況でよく使われます。  
  
- ワークグループがある場合。  
  
- ユーザーが、信頼されていない別のドメインから接続する。  
  
- ASP.NET などのインターネット アプリケーション。  
  
> [!NOTE]
> Windows 認証を指定しても、SQL Server ログインは無効になりません。 高い権限を持つ SQL Server ログインを無効にするには、Transact-SQL ステートメント ALTER LOGIN DISABLE を使用します。  
  
## <a name="login-types"></a>ログインの種類  
SQL Server では、次の 3 種類のログインがサポートされています。  
  
- ローカル Windows ユーザー アカウントまたは信頼される側のドメイン アカウント。 SQL Server が Windows に依存する形で Windows ユーザー アカウントを認証します。  
  
- Windows グループ。 Windows グループへのアクセス権を付与すると、そのグループのメンバーであるすべての Windows ユーザー ログインへのアクセス権が付与されます。  
  
- SQL Server ログイン SQL Server はユーザー名およびパスワードのハッシュを master データベースに格納し、内部の認証方法を使ってログイン試行を検証します。  
  
> [!NOTE]
> SQL Server では、証明書または非対称キーから作成されたログインが提供されています。このログインはコード署名にのみ使用されます。 SQL Server への接続には使用できません。  
  
## <a name="mixed-mode-authentication"></a>混合モード認証  
混合モード認証を使用する場合は、SQL Server に格納される SQL Server ログインを作成する必要があります。 さらに、SQL Server のユーザー名とパスワードを実行時に指定する必要があります。  
  
> [!IMPORTANT]
> SQL Server は、`sa` ("system administrator" の略) という名前の SQL Server ログインでインストールされます。 `sa` ログインに強力なパスワードを割り当て、アプリケーションで `sa` ログインを使用しないでください。 `sa` ログインは `sysadmin` 固定サーバー ロールにマップされます。このロールには、サーバー全体に対する取り消し不可能な管理者資格情報が割り当てられています。 攻撃者がシステム管理者としてアクセス権を獲得した場合、損害の可能性はとどまることがありません。 既定では、Windows `BUILTIN\Administrators` グループ (ローカル管理者のグループ) のすべてのメンバーが `sysadmin` ロールに所属しますが、そのロールから削除することもできます。  
  
> [!IMPORTANT]
> ユーザー入力から接続文字列を連結することによって、接続文字列インジェクションの攻撃に晒される可能性があります。 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> を使用して、実行時に構文的に有効な接続文字列を作成します。 
  
## <a name="external-resources"></a>外部リソース  
詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|[プリンシパル](../../../relational-databases/security/authentication-access/principals-database-engine.md)|SQL Server のログインおよびその他のセキュリティ プリンシパルについて説明します。|  
  
## <a name="next-steps"></a>次のステップ
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-sql-server.md)
