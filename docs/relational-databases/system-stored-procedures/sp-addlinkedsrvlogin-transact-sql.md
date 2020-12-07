---
description: sp_addlinkedsrvlogin (Transact-sql)
title: sp_addlinkedsrvlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlinkedsrvlogin_TSQL
- sp_addlinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedsrvlogin
ms.assetid: eb69f303-1adf-4602-b6ab-f62e028ed9f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4658625065876f35e3eb892381be67226795584f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548435"
---
# <a name="sp_addlinkedsrvlogin-transact-sql"></a>sp_addlinkedsrvlogin (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のローカルインスタンス上のログイン [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とリモートサーバー上のセキュリティアカウントとの間のマッピングを作成または更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_addlinkedsrvlogin [ @rmtsrvname = ] 'rmtsrvname'   
     [ , [ @useself = ] { 'TRUE' | 'FALSE' | NULL } ]   
     [ , [ @locallogin = ] 'locallogin' ]   
     [ , [ @rmtuser = ] 'rmtuser' ]   
     [ , [ @rmtpassword = ] 'rmtpassword' ]   
```  
  
## <a name="arguments"></a>引数  
 `[ @rmtsrvname = ] 'rmtsrvname'`  
 ログインマッピングが適用されるリンクサーバーの名前を指定します。 *rmtsrvname* は **sysname**,、既定値はありません。  
  
 `[ @useself = ] { 'TRUE' | 'FALSE' | NULL }'`  
 ローカルログインの権限を借用するか、ログインとパスワードを明示的に送信することで、 *rmtsrvname* に接続するかどうかを決定します。 データ型は **varchar (** 8 **)**,、既定値は TRUE です。  
  
 値が TRUE の場合は、ログインが独自の資格情報を使用して *rmtsrvname*に接続することを指定します。 *rmtuser* と *rmtpassword* 引数は無視されます。 FALSE を指定すると、 *rmtuser*と*rmtuser*引数を使用して、指定された*locallogin*の*rmtsrvname*に接続します。 *Rmtuser*と*RMTUSER*も NULL に設定されている場合は、リンクサーバーへの接続にログインまたはパスワードは使用されません。  
  
 `[ @locallogin = ] 'locallogin'`  
 ローカルサーバー上のログインを示します。 *locallogin* は **sysname**,、既定値は NULL です。 NULL は、このエントリが *rmtsrvname*に接続するすべてのローカルログインに適用されることを指定します。 NULL 以外の場合、 *locallogin* はログインまたは Windows ログインにすることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 Windows ログインに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、直接、または windows グループのメンバーシップによってアクセスが許可されている必要があります。  
  
 `[ @rmtuser = ] 'rmtuser'`  
 が FALSE の場合に *rmtsrvname* に接続するために使用されるリモートログインを指定し @useself ます。 リモートサーバーが Windows 認証を使用しないのインスタンスである場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 *rmtuser* は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインです。 *rmtuser* は **sysname**,、既定値は NULL です。  
  
 `[ @rmtpassword = ] 'rmtpassword'`  
 *Rmtuser*に関連付けられているパスワードを入力します。 *rmtpassword* の型は **sysname**で、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 ユーザーがローカルサーバーにログオンし、リンクサーバー上のテーブルにアクセスする分散クエリを実行する場合、ローカルサーバーは、そのテーブルにアクセスするために、ユーザーに代わってリンクサーバーにログオンする必要があります。 sp_addlinkedsrvlogin を使用して、ローカル サーバーがリンク サーバーへのログインに使用するログイン資格情報を指定します。  
  
> [!NOTE]  
>  リンクサーバー上のテーブルを使用しているときに最適なクエリプランを作成するには、クエリプロセッサにリンクサーバーからのデータ分布統計が必要です。 テーブルの列に対する権限が制限されているユーザーには、すべての有用な統計情報を取得するための十分な権限がない可能性があります。また、クエリプランの効率が低下し、パフォーマンスが低下する可能性があります。 リンク サーバーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスである場合、利用可能な統計情報をすべて取得するには、ユーザーがテーブルを所有しているか、リンク サーバーの固定サーバー ロール sysadmin、固定データベース ロール db_owner、または固定データベース ロール db_ddladmin のメンバーである必要があります。 SQL Server 2012 SP1 では、統計を取得するための権限の制限が変更され、SELECT 権限を持つユーザーは DBCC SHOW_STATISTICS で入手可能な統計にアクセスできます。 詳細については、「 [DBCC SHOW_STATISTICS &#40;transact-sql&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)」の「権限」セクションを参照してください。  
  
 sp_addlinkedserver を実行することにより、ローカル サーバー上のすべてのログインとリンク サーバー上のリモート ログインとの間の既定のマッピングが自動的に作成されます。 既定のマッピングでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの代わりにリンクサーバーに接続するときに、ローカルログインのユーザー資格情報が使用されます。 これは、 @useself ローカルユーザー名を指定せずに、リンクサーバーのを **true** に設定して sp_addlinkedsrvlogin を実行することと同じです。 既定のマッピングを変更するときや、特定のローカル ログインに対応する新しいマッピングを追加するときだけ sp_addlinkedsrvlogin を使用します。 既定のマッピングまたはその他のマッピングを削除するには、sp_droplinkedsrvlogin を使用します。  
  
 次のすべての条件が成立する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、sp_addlinkedsrvlogin を使用してあらかじめ決められたログイン マッピングを作成する代わりに、クエリを実行するユーザーの Windows セキュリティ資格情報 (Windows のログイン名とパスワード) を自動的に使用して、リンク サーバーに接続できます。  
  
-   ユーザーが Windows 認証モードを使用してに接続されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   クライアントと送信側のサーバーで、セキュリティアカウントの委任を使用できます。  
  
-   たとえば Windows 上で実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のように、プロバイダーが Windows 認証モードをサポートしている。  
  
> [!NOTE]  
>  シングルホップのシナリオでは委任を有効にする必要はありませんが、複数ホップのシナリオでは必須です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンス上で sp_addlinkedsrvlogin を実行して定義されたマッピングを、リンク サーバーが使用して認証を行った後は、ローカル サーバーではなく、リンク サーバーがリモート データベース内の個々のオブジェクトに対する権限を規定します。  
  
 ユーザー定義のトランザクション内から sp_addlinkedsrvlogin を実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する ALTER ANY LOGIN 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-connecting-all-local-logins-to-the-linked-server-by-using-their-own-user-credentials"></a>A. 独自のユーザー資格情報を使用して、すべてのローカルログインをリンクサーバーに接続する  
 次の例では、ローカルサーバーへのすべてのログインが、 `Accounts` 独自のユーザー資格情報を使用してリンクサーバーに接続するように、マッピングを作成します。  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts';  
```  
  
 または  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'true';  
```  
  
> [!NOTE]  
>  個々のログインに対して明示的なマッピングが作成されている場合は、そのリンクサーバーに存在する可能性のあるグローバルマッピングよりも優先されます。  
  
### <a name="b-connecting-a-specific-login-to-the-linked-server-by-using-different-user-credentials"></a>B. 異なるユーザー資格情報を使用して特定のログインをリンクサーバーに接続する  
 次の例では、マッピングを作成して、Windows ユーザーが `Domain\Mary` `Accounts` ログインとパスワードを使用してリンクサーバーに接続できるようにし `MaryP` `d89q3w4u` ます。  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'false', 'Domain\Mary', 'MaryP', 'd89q3w4u';  
```  
  
> [!IMPORTANT]  
>  この例では、Windows 認証を使用しません。 パスワードは暗号化されずに送信されます。 パスワードは、ディスク、バックアップ、およびログファイルに保存されたデータ ソース定義やスクリプトで参照できます。 この種類の接続では、システム管理者のパスワードを使用しないでください。 環境に固有のセキュリティガイダンスについては、ネットワーク管理者に問い合わせてください。  
  
## <a name="see-also"></a>参照  
 [リンクサーバーのカタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
