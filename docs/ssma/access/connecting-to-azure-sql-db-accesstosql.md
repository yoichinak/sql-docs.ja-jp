---
title: Azure SQL Database への接続 (SQL server への接続) |Microsoft Docs
description: Azure SQL Database のターゲットインスタンスに接続して Access データベースを移行する方法について説明します。 SSMA は Azure SQL Database のデータベースに関するメタデータを取得します。
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f910e9c07bf4318419714b97e4f4db742c913753
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869470"
---
# <a name="connecting-to-azure-sql-database-accesstosql"></a>Azure SQL Database への接続 (SQL server)

Access データベースをに移行するには [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、の対象インスタンスに接続する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 接続すると、SSMA はインスタンス内のすべてのデータベースに関するメタデータ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] を取得し、 **Azure SQL Database メタデータエクスプローラー** にデータベースのメタデータを表示します。 SSMA は、接続されているのインスタンスに関する情報を格納し [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ますが、パスワードは保存しません。

への接続 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、サーバーへのアクティブな接続が必要な場合は、に再接続する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 データベースオブジェクトをに読み込んでデータを移行するまで、オフラインで作業することができ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

のインスタンスに関するメタデータ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は、自動的には同期されません。 代わりに、メタデータ **エクスプローラー Azure SQL Database** メタデータを更新するには、メタデータを手動で更新する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 詳細については、このトピックで後述する「Azure SQL Database メタデータの同期」を参照してください。

## <a name="required-azure-sql-database-permissions"></a>必要な Azure SQL Database アクセス許可

への接続に使用するアカウントには、 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] アカウントが実行するアクションに応じて、異なるアクセス許可が必要です。

- Access オブジェクトを構文に変換し [!INCLUDE[tsql](../../includes/tsql-md.md)] たり、からメタデータを更新したり、変換され [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] た構文をスクリプトに保存したりするには、アカウントにのインスタンスにログオンする権限が必要 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] です。

- データベースオブジェクトをに読み込むには、 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] アカウントが **db_ddladmin** データベースロールのメンバーである必要があります。

- にデータを移行するには、 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] アカウントが **db_owner** データベースロールのメンバーである必要があります。

## <a name="establishing-an-azure-sql-database-connection"></a>Azure SQL Database 接続の確立

Access データベースオブジェクトを構文に変換する前に [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、access データベースの移行先となるのインスタンスへの接続を確立する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

接続プロパティを定義するときに、オブジェクトとデータを移行するデータベースも指定します。 このマッピングは、に接続した後、Access スキーマレベルでカスタマイズでき [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 詳細については、「 [Access データベースの SQL Server スキーマへのマッピング」を](mapping-source-and-target-databases-accesstosql.md)参照してください。
  
> [!IMPORTANT]
> に接続する前に [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、ファイアウォール経由で IP アドレスが許可されていることを確認してください [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。
  
[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] に接続するには次の操作を行います。

1. [ **ファイル** ] メニューの [ **SQL Azure に接続** ] を選択します (このオプションは、プロジェクトの作成後に有効になります)。
   以前にに接続していた場合 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、コマンド名は **SQL Azure に再接続** されます。

2. [接続] ダイアログボックスで、のサーバー名を入力または選択し [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

3. データベース名を入力、選択、または **参照** します。

4. [ **ユーザー名**] を入力または選択します。

5. **パスワード** を入力します。

6. SSMA では、への暗号化接続を推奨 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] しています。

7. **[Connect]** をクリックします。
  
にデータベースが存在しない場合は、 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] [**参照** のクリック] ボタンに表示される [ **Azure データベースの作成**] オプションを使用して最初のデータベースを作成できます。

## <a name="synchronizing-azure-sql-database-metadata"></a>Azure SQL Database メタデータの同期

のデータベースに関するメタデータ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は自動的に更新されません。 **Azure SQL Database メタデータエクスプローラー** のメタデータは、最初に接続したとき [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、またはメタデータを手動で更新したときにメタデータのスナップショットになります。 すべてのデータベース、または任意の1つのデータベースまたはデータベースオブジェクトのメタデータを手動で更新できます。 メタデータを同期するには:

1. に接続されていることを確認し [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

2. **Azure SQL Database メタデータエクスプローラー** で、更新するデータベースまたはデータベーススキーマの横にあるチェックボックスをオンにします。
   たとえば、すべてのデータベースのメタデータを更新するには、[ **データベース**] の横にあるチェックボックスをオンにします。

3. [データベース]、または個々のデータベースまたはデータベーススキーマを **右クリックし**、[ **データベースとの同期**] を選択します。

## <a name="refreshing-azure-sql-database-metadata"></a>Azure SQL Database メタデータの更新

[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]接続後にスキーマが変更された場合は、サーバーからメタデータを更新できます。

メタデータを更新するに [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は:

- **Azure SQL Database メタデータエクスプローラー** で、[**データベース**] を右クリックし、[**データベースから更新**] を選択します。

## <a name="reconnecting-to-azure-sql-database"></a>Azure SQL Database に再接続しています

への接続 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、サーバーへのアクティブな接続が必要な場合は、に再接続する必要があり [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。 データベースオブジェクトをに読み込んでデータを移行するまで、オフラインで作業することができ [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

に再接続する手順 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] は、接続を確立する手順と同じです。

## <a name="next-steps"></a>次のステップ

移行の次のステップは、プロジェクトのニーズによって異なります。

- アクセススキーマと Azure SQL Database 間のマッピングをカスタマイズするには、「 [SQL Server スキーマへの Access データベースのマッピング](mapping-source-and-target-databases-accesstosql.md)」を参照してください。
- プロジェクトの構成オプションをカスタマイズするには、「 [プロジェクトオプションの設定](setting-conversion-and-migration-options-accesstosql.md)」を参照してください。
- ソースとターゲットのデータ型のマッピングをカスタマイズするには、「 [ソースとターゲットのデータ型のマッピング](mapping-source-and-target-data-types-accesstosql.md)」を参照してください。
- これらのタスクを実行する必要がない場合は、Access データベースオブジェクト定義を SQL Azure オブジェクト定義に変換できます。 詳細については、「 [Access データベースの変換](converting-access-database-objects-accesstosql.md)」を参照してください。

## <a name="see-also"></a>参照

[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)
