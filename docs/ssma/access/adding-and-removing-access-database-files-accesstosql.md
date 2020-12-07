---
title: Access データベースファイルの追加と削除 (アクセス権限のある Sql) |Microsoft Docs
description: SSMA プロジェクトとの間でアクセスデータベースを追加または削除して SQL Server または Azure SQL Database にアクセスデータを移行する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 12c51ce9a3b4bdd83a1d1c4c7295f2ff438bc707
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987718"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Access データベースファイルの追加と削除 (アクセス許可 Sql)
アクセスデータをまたは SQL Azure に移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、SSMA プロジェクトに1つ以上の access データベースを追加する必要があります。 これらのデータベースは、97以降のバージョンにアクセスする必要があります。 以前のバージョンの Access のデータベースがある場合は、データベースを新しいバージョンに変換する必要があります。 これを行うには、データベースを SSMA に追加する前に Access 97 以降のバージョンで開いて保存します。  
  
## <a name="what-happens-when-you-add-access-database-files"></a>Access データベースファイルを追加するとどうなりますか。  
SSMA プロジェクトに Access データベースを追加すると、SSMA はデータベースメタデータを読み取り、このメタデータをプロジェクトファイルに追加します。 このメタデータは、データベースとそのオブジェクトを記述します。 SSMA では、オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure 構文に変換するときや、データをまたは SQL Azure に移行するときに、メタデータを使用し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このメタデータは、Access メタデータエクスプローラーで参照し、個々のデータベースオブジェクトのプロパティを確認できます。  
  
> [!NOTE]  
> Access データベースは、複数のファイルに分割できます。テーブルを格納するバックエンドデータベースと、クエリ、フォーム、レポート、マクロ、モジュール、およびショートカットを含むフロントエンドデータベースです。 分割されたデータベースをまたは SQL Azure に移行する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、フロントエンドデータベースを SSMA に追加します。  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA に必要なアクセス許可  
Access データベースをまたは SQL Azure に移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、Users グループと管理者ユーザーが管理アクセス許可を持っている必要があります。 ワークグループ保護を使用してデータベースを移行する方法については、「 [Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)」を参照してください。  
  
## <a name="selecting-databases-to-add"></a>追加するデータベースの選択  
SSMA プロジェクトに1つ以上のデータベースを追加する場合に、ファイルがすべて既知の場所にある場合は、次の手順を使用してファイルを追加できます。  
  
**個々のデータベースファイルを追加するには**  
  
1.  [ **ファイル** ] メニューの [ **データベースの追加**] をクリックします。  
  
2.  [ **開く** ] ダイアログボックスで、データベースファイルが格納されているフォルダーに移動します。  
  
3.  追加するファイルを選択し、[ **開く**] をクリックします。  
  
## <a name="finding-databases-to-add"></a>追加するデータベースの検索  
複数の Access データベースを別のフォルダーから SSMA プロジェクトに追加する場合、または1つのファイルを追加する必要があり、ファイルを検索する必要がある場合は、次の手順に従って、ファイルの1つを検索してプロジェクトに追加します。  
  
**データベースを検索して追加するには**  
  
1.  [ **ファイル** ] メニューの [ **データベースの検索**] をクリックします。  
  
2.  [データベースの検索] ウィザードで、検索するドライブ、ファイルパス、または UNC パスの名前を入力します。 または、[ **参照** ] をクリックして、ドライブまたはネットワークフォルダーを指定します。  
  
3.  [ **追加** ] をクリックして、一覧に場所を追加します。  
  
    前の2つの手順を繰り返して、検索場所を追加します。  
  
4.  必要に応じて、検索条件を追加して、返されるデータベースの一覧を絞り込むことができます。  
  
    > [!IMPORTANT]  
    > [ **ファイル名] テキストボックスの全体または一部** がワイルドカード文字をサポートしていません。  
  
5.  **[スキャン]** をクリックします。  
  
    スキャンページが表示されます。 これにより、検出されたデータベースと検索の進行状況が表示されます。 検索を停止するには、[ **停止**] をクリックします。  
  
6.  [ファイルの選択] ページで、プロジェクトに追加するデータベースを選択します。  
  
    すべてのデータベースを選択または選択解除するには、一覧の上部にある **[すべて選択]** ボタンと [ **すべてクリア** ] ボタンを使用します。 CTRL キーを押しながら複数のデータベースを選択するか、SHIFT キーを押しながらデータベースの範囲を選択できます。  
  
7.  **[次へ]** をクリックします。  
  
8.  [確認] ページで、[ **完了**] をクリックします。  
  
## <a name="browsing-access-metadata"></a>参照 (アクセスメタデータを)  
Access データベースをプロジェクトに追加すると、Access メタデータエクスプローラーにプロジェクトのメタデータが表示されます。 エクスプローラーで、データベースとデータベースオブジェクトの階層を参照できます。  
  
**メタデータを参照するには**  
  
1.  Access Metadata Explorer で、[ **アクセス-メタベース**] を展開し、[ **データベース**] を展開します。  
  
2.  確認するデータベースを展開し、[ **クエリ**] を展開します。  
  
    クエリの一覧に注意してください。 クエリを選択すると、右側のペインに [ **SQL** ] タブと [ **プロパティ** ] タブが表示されます。  
  
3.  [ **テーブル** ] を展開し、テーブルを選択します。  
  
    [ **テーブル**]、[ **型マッピング**]、[ **プロパティ**]、[ **データ**] の4つのタブが表示されます。  
  
4.  テーブルを展開し、[ **キー**] を展開して、キーを選択します。  
  
    キープロパティが右ペインに表示されます。  
  
5.  [ **インデックス**] を展開し、インデックスを選択します。  
  
    右ペインにインデックスのプロパティが表示されます。  
  
## <a name="refreshing-databases"></a>データベースの更新  
ファイルを追加した後に Access データベースが変更された場合は、Access データベースからメタデータを更新できます。  
  
**アクセスメタデータを更新するには**  
  
-   Access Metadata Explorer で、データベースを右クリックし、[ **データベースから更新**] を選択します。  
  
## <a name="removing-databases"></a>データベースの削除  
次の手順に従って、プロジェクトから Access データベースを削除できます。  
  
**プロジェクトからデータベースを削除するには**  
  
1.  Access Metadata Explorer で、[ **アクセス-メタベース**] を展開し、[ **データベース**] を展開します。  
  
2.  データベースを右クリックし、[データベースの **削除**] を選択します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順では、 [SQL Server に接続](../sybase/connecting-to-sql-server-sybasetosql.md)します。  
  
## <a name="see-also"></a>参照  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[プロジェクトの作成と管理](creating-and-managing-projects-accesstosql.md)  
