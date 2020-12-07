---
title: SQL Database プロジェクトの拡張機能をお使いになる前に
description: Azure Data Studio の SQL データベース プロジェクトの拡張機能の使用を開始する
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 07/30/2020
ms.openlocfilehash: cd818010b068ccd206f411ce8c578386d0b8772f
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123366"
---
# <a name="getting-started-with-the-sql-database-projects-extension-preview"></a>SQL Database プロジェクトの拡張機能をお使いになる前に (プレビュー)

この記事では、SQL Database プロジェクト拡張機能の使用を開始する 3 つの方法について説明します。

1. 新しいデータベース プロジェクトを作成するには、エクスプローラーの下の **プロジェクト** viewlet に移動するか、コマンド パレットで**新しいデータベース プロジェクト**を検索します。
2. 既存のデータベース プロジェクトは、コマンド パレットで **[Open Database Project]\(データベース プロジェクトを開く\)** を使用して開くことができます。
3. コマンド パレットから **[Import New Database Project]\(新しいデータベース プロジェクトをインポート\)** を使用して、既存のデータベースから開始します。

    ![新しい viewlet](media/sql-database-projects-extension/projects-viewlet.png)

## <a name="create-an-empty-database-project"></a>空のデータベース プロジェクトを作成する

**エクスプローラー**の下の**プロジェクト** viewlet で、 **[新しいプロジェクト]** ボタンを選択し、表示されるテキスト入力にプロジェクト名を入力します。  表示される [フォルダーの選択] ダイアログ ボックスで、プロジェクトのフォルダー、.sqlproj ファイル、およびそこに含まれるその他の内容を選択します。
空のプロジェクトが開き、編集のために **プロジェクト** viewlet に表示されます。

## <a name="open-an-existing-project"></a>既存のプロジェクトを開く

**プロジェクト** viewlet で、 **[プロジェクトを開く]** ボタンを選択し、表示されたファイル ピッカーから既存の *.sqlproj* ファイルを開きます。 既存のプロジェクトは、Azure Data Studio または [Visual Studio SQL Server Data Tools](../../ssdt/sql-server-data-tools.md) から作成できます。

既存のプロジェクトが開かれ、編集のためにその内容が **プロジェクト** viewlet に表示されます。

## <a name="create-a-database-project-from-an-existing-database"></a>既存のデータベースからデータベース プロジェクトを作成する

**プロジェクト** viewlet で、 **[Import Project from Database]\(データベースからプロジェクトをインポート\)** ボタンを選択して SQL Server に接続します。  接続が確立されたら、使用可能なデータベースのリストからデータベースを選択し、プロジェクトの名前を設定します。

最後に、抽出のターゲット構造を選択します。  新しいプロジェクトが開き、選択したデータベースの内容に対応する SQL スクリプトが含まれます。

## <a name="build-and-publish"></a>ビルドして発行する

データベース プロジェクトのデプロイは、Azure Data Studio の SQL Database プロジェクトの拡張機能でプロジェクトを[データ層アプリケーション ファイル](../../relational-databases/data-tier-applications/data-tier-applications.md) (DACPAC) にビルドし、サポートされているプラットフォームに発行することで実現されます。 このプロセスの詳細については、「[プロジェクトをビルドして公開する](sql-database-project-extension-build.md)」を参照してください。

## <a name="schema-compare"></a>スキーマの比較

SQL Database プロジェクトの拡張機能は、[Schema Compare の拡張機能](schema-compare-extension.md)がインストールされている場合はそれとやり取りして、プロジェクトの内容を dacpac または既存のデータベースと比較します。  結果として得られるスキーマ比較を使用して、ソースとターゲットの違いを表示し、適用することができます。

## <a name="next-steps"></a>次のステップ

- [Azure Data Studio の SQL Database プロジェクトの拡張機能を使用してプロジェクトをビルドして発行する](sql-database-project-extension-build.md)