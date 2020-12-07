---
description: 移行ウィザード (移動用 Sql)
title: 移行ウィザード (移動用 Sql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: c8f03fa27bf8c49cfeef06246c47996860c932ba
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988650"
---
# <a name="migration-wizard-accesstosql"></a>移行ウィザード (移動用 Sql)
移行ウィザードでは、または SQL Azure へのアクセスから、1つまたは複数のデータベースを移行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 ウィザードを使用して、プロジェクトを作成し、データベースをプロジェクトに追加し、移行するオブジェクトを選択して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure に接続します。 また、アクセススキーマとデータの変換、読み込み、移行を行います。 必要に応じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたは SQL Azure テーブルにアクセステーブルをリンクすることもできます。  
  
移行ウィザードのほとんどのページには、既存の SSMA ダイアログボックスと同じオプションが含まれています。 そのため、ここではウィザードのページについて説明します。また、各オプションの詳細については、リンクが用意されています。 ページに一意のオプションが含まれている場合は、ここに記載されています。  
  
## <a name="starting-the-migration-wizard"></a>移行ウィザードを開始しています  
既定では、SSMA の起動時に移行ウィザードが表示されます。 また、[ **ファイル** ] メニューの [ **移行ウィザード**] を選択して、ウィザードを起動することもできます。  
  
## <a name="welcome-page"></a>ウェルカム ページ  
[ようこそ] ページには、移行ウィザードが導入されており、ウィザードを起動するための次のオプションが用意されています。  
  
**起動時にこのウィザードを起動します。**  
既定では、ssma の起動時に移行ウィザードが開始されます。 ウィザードが自動的に開始されないようにするには、このチェックボックスをオフにします。  
  
## <a name="create-new-project-page"></a>[新しいプロジェクトの作成] ページ  
[新しいプロジェクトの作成] ページには、プロジェクトのファイル名、場所と移行プロジェクトの種類 (移行に使用するターゲット SQL Server のバージョン) を入力します。 詳細については、「[新しいプロジェクト (SSMA)](./new-project-ssma-accesstosql.md) 」を参照してください。  
  
## <a name="add-access-databases-page"></a>[Access データベースの追加] ページ  
[Access データベースの追加] ページでは、プロジェクトに1つ以上の Access データベースを追加します。 個々のデータベースを追加するには、[ **データベースの追加**] をクリックし、[ **開く** ] ウィンドウからデータベースを選択します。 または、[ **データベースの検索** ] ボタンを使用してデータベースを検索することもできます。 詳細については、次のトピックを参照してください。  
  
-   [Access データベースファイルの追加と削除](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [データベースのウィザードを検索 (場所の選択)](./find-databases-wizard-select-locations-accesstosql.md)  
  
-   [データベースのウィザードを検索 (ファイルの選択)](./find-databases-wizard-select-files-accesstosql.md)  
  
-   [データベースのウィザードを検索 (選択の確認)](./find-databases-wizard-verify-selection-accesstosql.md)  
  
## <a name="select-objects-to-migrate-page"></a>[移行するオブジェクトの選択] ページ  
[移行するオブジェクトの選択] ページで、変換するオブジェクトを選択します。 すべてのオブジェクト、オブジェクトのグループ、または個々のオブジェクトを選択できます。  
  
**オブジェクトを選択するには**  
  
1.  [ **アクセス-メタベース**] を展開し、[ **データベース**] を展開します。  
  
2.  次のうち1 つ以上を行います。  
  
    -   すべてのデータベースを変換するには、[ **データベース**] の横にあるチェックボックスをオンにします。  
  
    -   個々のデータベースを変換または除外するには、データベース名の横にあるチェックボックスをオンまたはオフにします。  
  
    -   クエリを変換または省略するには、データベースを展開し、[ **クエリ** ] チェックボックスをオンまたはオフにします。  
  
    -   個々のテーブルを変換または省略するには、データベースを展開し、[ **テーブル**] を展開して、テーブルの横にあるチェックボックスをオンまたはオフにします。  
  
多数のオブジェクトがある場合は、右側のウィンドウにある **[高度なオブジェクトの選択** ] オプションを使用して、Access データベースオブジェクトをフィルター処理することをお勧めします。 たとえば、左側のペインで [ **テーブル** ] を選択した場合、[ **フィルター** ] ボックスに文字列を入力すると、テーブルの一覧をフィルター処理できます。 次に、ペインの上部にあるボタンを使用して、フィルター選択されたテーブルを選択またはオフにします。  
  
フィルター処理の詳細については、「 [高度なオブジェクトの選択 (SSMA Common)](../sybase/advanced-object-selection-sybasetosql.md)」の「オプション」セクションを参照してください。  
  
## <a name="connect-to-sql-server-page"></a>SQL Server ページに接続する  
[接続先 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ] ページで、接続プロパティを指定し、に接続し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [SQL Server への接続](connect-to-sql-server-accesstosql.md)」を参照してください。
  
> [!IMPORTANT]  
> 接続が成功するとすぐに [テーブルの **リンク** ] ページが表示され、そこにテーブルをリンクするオプションが表示されます。 [ **次へ** ] をクリックして、移行を開始します。  
  
## <a name="connect-to-sql-azure-page"></a>SQL Azure ページに接続する  
[SQL Azure への接続] ページで、接続プロパティを指定し、SQL Azure に接続します。 新しい Azure データベースを作成するには、[**参照**のクリック] ボタンに表示される [ **Azure データベースの作成**] オプションを使用します。 詳細については、「 [Connect to SQL Azure](connect-to-azure-sql-db-accesstosql.md) 」を参照してください。  
  
> [!IMPORTANT]  
> 接続が成功するとすぐに [テーブルの **リンク** ] ページが表示され、そこにテーブルをリンクするオプションが表示されます。 [リンク] ページの [ **次へ** ] ボタンをクリックして、移行を開始します。  
  
## <a name="link-tables-page"></a>[テーブルのリンク] ページ  
[テーブルのリンク] ページを使用すると、元の Access テーブルを、移行された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたは SQL Azure テーブルにリンクすることができます。 テーブルをリンクすると、access データベースが変更されます。これにより、クエリ、フォーム、レポート、およびデータアクセスページで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] access データベースのデータではなく、または Azure SQL Database のデータが使用されるようになります。  
  
**リンクテーブル**  
[ **テーブルのリンク** ] チェックボックスをオンにすると、移行された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたは SQL Azure テーブルにアクセステーブルをリンクできます。 移行を開始するには、[ **次へ** ] ボタンをクリックする必要があります。  
  
## <a name="migration-status-page"></a>[移行の状態] ページ  
[移行の状態] ページには、または SQL Azure スキーマへのアクセススキーマの変換 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、変換されたスキーマのまたは SQL Azure への読み込み、データの移行の進行状況が表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
このページの詳細については、「[変換、読み込み、移行](./convert-load-and-migrate-accesstosql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[アクセスのための SQL Server Migration Assistant を使用したはじめに &#40;アクセス許可 SQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[ユーザーインターフェイスリファレンス (アクセス)](./user-interface-reference-accesstosql.md)  
