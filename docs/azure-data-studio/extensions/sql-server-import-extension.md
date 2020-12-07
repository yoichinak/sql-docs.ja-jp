---
title: SQL Server インポートの拡張機能
description: .txt ファイルと .csv ファイルを SQL テーブルに変換するウィザードである、Azure Data Studio 用の SQL Server インポート拡張機能をインストールして使用する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: caf2b3ee70d2542dc529e83e1e243ff215c644a4
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123230"
---
# <a name="sql-server-import-extension"></a>SQL Server インポートの拡張機能

SQL Server インポートの拡張機能を使用すると、.txt ファイルと .csv ファイルが SQL テーブルに変換されます。 このウィザードでは、[Program Synthesis using Examples (PROSE)](https://microsoft.github.io/prose/) と呼ばれるマイクロソフト リサーチ フレームワークを利用して、最小のユーザー入力でファイルをインテリジェントに解析することができます。 これはデータ ラングリングの強力なフレームワークであり、Microsoft Excel でフラッシュ フィルを強化するテクノロジと同じです。

この機能の SSMS バージョンの詳細については、[こちら](../../relational-databases/import-export/import-flat-file-wizard.md)の記事を参照してください。

## <a name="install-the-sql-server-import-extension"></a>SQL Server インポートの拡張機能をインストールする

1. 拡張機能マネージャーを開いて、使用可能な拡張機能にアクセスするには、拡張機能アイコンを選択するか、 **[表示]** メニューの **[拡張機能]** を選択します。
2. 使用可能な拡張機能を選択すると、その詳細が表示されます。

   ![拡張機能マネージャーをインポートする](media/sql-server-import-extension/import-wizard-install.png)

3. 必要な拡張機能を選択して**インストール**します。
4. **[再読み込み]** を選択して拡張機能を有効にします (拡張機能を初めてインストールするときにのみ必要です)。

## <a name="start-import-wizard"></a>インポート ウィザードを開始する

1. SQL Server インポートを開始するには、まず [サーバー] タブでサーバーへの接続を確立します。
2. 接続を確立したら、SQL テーブルにファイルをインポートするターゲット データベースにドリルダウンします。
3. データベースを右クリックし、 **[インポート ウィザード]** を選択します。

    ![インポート ウィザード](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>ファイルのインポート

1. 右クリックしてウィザードを起動すると、サーバーとデータベースは既に自動入力されています。 アクティブな接続が他にもある場合は、ドロップダウンで選択することができます。 

    **[参照]** を選択してファイルを選択します。 これでファイル名に基づいてテーブル名が自動的に入力されますが、それを自分で変更することもできます。

    既定では、スキーマは dbo になりますが、これは変更することができます。 **[次へ]** を選択して続行します。

    ![入力ファイル](media/sql-server-import-extension/import-wizard-input-file.png)

2. ウィザードでは、最初の 50 行に基づいてプレビューが生成されます。 このページでは、データが正確であることを確認します。他には操作は行いません。 **[次へ]** を選択して続行します。

    ![データのプレビュー](media/sql-server-import-extension/import-wizard-preview-data.png)

3. このページでは、列名またはデータ型を変更したり、主キーかどうか、または null を許容するかどうかを変更したりすることができます。 変更は必要なだけ行うことができます。 **[データのインポート]** を選択して続行します。

    ![列の変更](media/sql-server-import-extension/import-wizard-modify-columns.png)

4. このページには、選択したアクションの概要が表示されます。 ご利用のテーブルが正常に挿入されたかどうかを確認することもできます。

    変更が必要な場合は、 **[完了]、[前へ]** を順に選択するか、別のファイルをすばやくインポートするために **[Import new file]** \(新しいファイルのインポート\) を選択します。

    ![まとめ](media/sql-server-import-extension/import-wizard-summary.png)

5. ご利用のターゲット データベースを更新するか、テーブル名に対して SELECT クエリを実行することにより、テーブルが正常にインポートされたかどうかを確認します。

## <a name="next-steps"></a>次のステップ

- インポート ウィザードの詳細については、[こちら](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)のブログの投稿を参照してください。
- PROSE の詳細については、[こちら](https://microsoft.github.io/prose/)のドキュメントを参照してください。