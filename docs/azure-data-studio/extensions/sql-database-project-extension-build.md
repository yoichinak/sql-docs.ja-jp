---
title: プロジェクトをビルドして公開する
description: SQL Server データベース プロジェクトの拡張機能を使用してプロジェクトをビルドして公開する
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 06/25/2020
ms.openlocfilehash: 8bcc0e9d54c98c83e184c3ff957dbf35082ba673
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100048416"
---
# <a name="build-and-publish-a-project"></a>プロジェクトをビルドして公開する

Azure Data Studio の SQL データベース プロジェクトの拡張機能 (プレビュー) のビルド プロセスでは、Windows、macOS、Linux 環境で *dacpac* を作成できます。 プロジェクトは、公開プロセスを使用してローカルまたはクラウド環境にデプロイできます。

## <a name="prerequisites"></a>前提条件

- [Azure Data Studio の SQL データベース プロジェクトの拡張機能](sql-database-project-extension.md)のインストールと構成。

## <a name="build-a-database-project"></a>データベース プロジェクトをビルドする

 **[エクスプローラー]** の下の **[プロジェクト]** viewlet で、 *.sqlproj* ルート ノードを右クリックし、 **[ビルド]** を選択します。

 出力ウィンドウに、ビルド プロセスからの出力が自動的に表示されます。  ビルドが成功すると、次のメッセージが表示されます。 

 ``` ... exited with code: 0 ```

## <a name="publish-a-database-project"></a>データベース プロジェクトを公開する

ビルド プロセスによってプロジェクトが正常にコンパイルされたら、データベースを SQL Server インスタンスに公開できます。 データベース プロジェクトを公開するには、 **[エクスプローラー]** の下の **[プロジェクト]** viewlet で、 *.sqlproj* ルート ノードを右クリックし、 **[公開]** を選択します。

表示される **[データベースの公開]** ダイアログで、サーバー接続と作成するデータベース名を指定します。

## <a name="next-steps"></a>次のステップ

- [Azure Data Studio の SQL データベース プロジェクトの拡張機能](sql-database-project-extension.md)
- [コマンド ラインから SQL データベース プロジェクトをビルドする](sql-database-project-extension-build-from-command-line.md)
