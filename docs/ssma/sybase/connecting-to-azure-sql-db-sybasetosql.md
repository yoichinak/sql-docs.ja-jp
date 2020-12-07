---
description: Azure SQL Database への接続 (SybaseToSQL)
title: Azure SQL Database への接続 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f88b7b5357a61708910846f78c09f80e7c783957
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870422"
---
# <a name="connecting-to-azure-sql-database-sybasetosql"></a>Azure SQL Database への接続 (SybaseToSQL)

Sybase データベースをに移行するには [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、の対象インスタンスに接続する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 接続すると、SSMA はインスタンス内のすべてのデータベースに関するメタデータ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] を取得し、 **Azure SQL Database メタデータエクスプローラー** にデータベースのメタデータを表示します。 SSMA は、接続しているのインスタンスの情報を格納し [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ますが、パスワードは保存しません。

への接続 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、サーバーへのアクティブな接続が必要な場合は、に再接続する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 データベースオブジェクトをに読み込んでデータを移行するまで、オフラインで作業することができ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

のインスタンスに関するメタデータ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は、自動的には同期されません。 代わりに、メタデータ **エクスプローラー Azure SQL Database** メタデータを更新するには、メタデータを手動で更新する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 詳細については、このトピックで後述する「Azure SQL Database メタデータの同期」を参照してください。

## <a name="required-azure-sql-database-permissions"></a>必要な Azure SQL Database アクセス許可

への接続に使用するアカウントには、 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] アカウントが実行するアクションに応じて、異なるアクセス許可が必要です。

- ASE オブジェクトを構文に変換し [!INCLUDE[tsql](../../includes/tsql-md.md)] たり、からメタデータを更新したり、変換され [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] た構文をスクリプトに保存したりするには、アカウントがのインスタンスにログオンする権限を持っている必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

- データベースオブジェクトをに読み込むには、 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] アカウントが **db_ddladmin** データベースロールのメンバーである必要があります。

- にデータを移行するには、 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] アカウントが **db_owner** データベースロールのメンバーである必要があります。

- SSMA によって生成されるコードを実行するには、 `EXECUTE` 対象データベースの **ssma_syb** スキーマに含まれるすべてのユーザー定義関数に対する権限がアカウントに付与されている必要があります。 これらの関数は、ASE システム関数と同等の機能を提供し、変換されたオブジェクトによって使用されます。

## <a name="establishing-an-azure-sql-database-connection"></a>Azure SQL Database 接続の確立

Sybase データベースオブジェクトを構文に変換する前に、Sybase データベースの移行先となる [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] のインスタンスへの接続を確立する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

接続プロパティを定義するときに、オブジェクトとデータを移行するデータベースも指定します。 このマッピングは、Azure SQL Database に接続した後に Sybase スキーマレベルでカスタマイズできます。 詳細については、「 [SQL Server スキーマ &#40;SybaseToSQL&#41;に SYBASE ASE スキーマをマップする ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)」を参照してください。

> [!IMPORTANT]
> に接続する前に [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、ファイアウォール経由で IP アドレスが許可されていることを確認してください [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。

[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] に接続するには次の操作を行います。

1. [ **ファイル** ] メニューの [ **Azure SQL Database に接続**] を選択します (このオプションは、プロジェクトの作成後に有効になります)。
   に既に接続している場合は [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、コマンド名が **Azure SQL Database に再接続** されます。

2. [接続] ダイアログボックスで、のサーバー名を入力または選択し [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

3. データベース名を入力、選択、または **参照** します。

4. [ **ユーザー名**] を入力または選択します。

5. **パスワード** を入力します。

6. SSMA では、への暗号化接続を推奨 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] しています。

7. **[Connect]** をクリックします。

## <a name="synchronizing-azure-sql-database-metadata"></a>Azure SQL Database メタデータの同期

データベースに関するメタデータ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は自動的に更新されません。 Azure SQL Database メタデータエクスプローラーのメタデータは、最初に Azure SQL Database に接続したとき、またはメタデータを手動で更新したときにメタデータのスナップショットになります。 すべてのデータベース、または任意の1つのデータベースまたはデータベースオブジェクトのメタデータを手動で更新できます。 メタデータを同期するには:

1. に接続されていることを確認し [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

2. **Azure SQL Database メタデータエクスプローラー** で、更新するデータベースまたはデータベーススキーマの横にあるチェックボックスをオンにします。
   たとえば、すべてのデータベースのメタデータを更新するには、[ **データベース**] の横にあるチェックボックスをオンにします。

3. [データベース]、または個々のデータベースまたはデータベーススキーマを **右クリックし**、[ **データベースとの同期**] を選択します。

## <a name="next-step"></a>次の手順

移行の次のステップは、プロジェクトのニーズによって異なります。

- Sybase スキーマとデータベースおよびスキーマ間のマッピングをカスタマイズするには [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、「 [Sybase ASE スキーマを SQL Server スキーマ &#40;SybaseToSQL&#41;にマップ ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)する」を参照してください。
- プロジェクトの構成オプションをカスタマイズするには、「 [SybaseToSQL&#41;&#40;プロジェクトオプションを設定 ](../../ssma/sybase/setting-project-options-sybasetosql.md)する」を参照してください。
- ソースとターゲットのデータ型のマッピングをカスタマイズするには、「 [SYBASE ASE と SQL Server のデータ型 &#40;SybaseToSQL&#41;のマッピング ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)」を参照してください。
- これらのタスクを実行する必要がない場合は、Sybase データベースオブジェクト定義をオブジェクト定義に変換でき [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 詳細については、「 [SYBASE ASE データベースオブジェクトの &#40;SybaseToSQL&#41;の変換 ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)」を参照してください。

## <a name="see-also"></a>参照

[Sybase ASE データベースを SQL Server Azure SQL Database &#40;SybaseToSQL&#41;に移行する ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
