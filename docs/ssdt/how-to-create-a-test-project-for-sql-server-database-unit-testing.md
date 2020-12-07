---
title: SQL Server の単体テストのテスト プロジェクトを作成する
description: SQL Server データベース単体テストのテスト プロジェクトを作成する方法について説明します。 データベース プロジェクトを含むソリューションにテスト プロジェクトを追加するさまざまな方法を確認します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 4b3e7ba8-b565-4689-af1a-34cc255b7c60
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: b5a10fdbc94858a9fe3f5b523fdd43b505e2563f
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987558"
---
# <a name="how-to-create-a-test-project-for-sql-server-database-unit-testing"></a>方法:SQL Server の単体テストのテスト プロジェクトを作成する

データベース オブジェクトを評価する単体テストの作成を開始する前に、まずはテスト プロジェクトを作成する必要があります。 このプロジェクトには SQL Server の単体テストが含まれていますが、他の種類のテストが含まれることもあります。  
  
特定のデータベース プロジェクトに対するすべての SQL Server の単体テストを 1 つのテスト プロジェクト内に配置することができます。 ただし、次の質問に対する回答に基づいて、追加のテスト プロジェクトの作成が必要になる場合もあります。  
  
|Question|決定|  
|-|-|   
|テストの実行やテストの検証のために、SQL Server の単体テストごとに異なるデータベース接続にアクセスする必要がありますか。|回答が "はい" の場合は、複数のテスト プロジェクトが必要です。 テストの実行には複数のデータベース接続を指定できません。 ただし、テストの検証には別のデータベース接続を指定できます。|  
|単体テストごとに異なるデータベース プロジェクトを配置しますか。|回答が "はい" の場合は、複数のテスト プロジェクトが必要です。 テスト プロジェクトによって配置できるのは 1 つのデータベース プロジェクトのみです。|  
  
これらの各質問の詳細については、「[SQL Server の単体テストの実行を構成する方法](../ssdt/how-to-configure-sql-server-unit-test-execution.md)」を参照してください。 複数のテスト プロジェクトを作成する代わりに、独自の [DatabaseTestService](/previous-versions/visualstudio/visual-studio-2010/dd154755(v=vs.100)) Microsoft.Data.Schema.UnitTesting.DatabaseTestService 実装を提供することもできます。  
  
データベース プロジェクトを含むソリューションにテスト プロジェクトを追加するには、次の 3 つの方法があります。  
  
-   ソリューションにテスト プロジェクトを追加する。 テスト プロジェクトには、標準的な単体テスト (削除可能) が含まれています。 このプロジェクトには、追加する必要がある SQL Server の単体テスト クラスが含まれていません。  
  
-   **[テスト]** メニューから新しい SQL Server の単体テストを追加する。 単体テストを追加するときに、指定した場合は SQL Server Data Tools によってテスト プロジェクトも作成されます。 このプロジェクトには、SQL Server 単体テスト クラスが含まれています。 SQL Server 単体テスト クラスには、1 つ以上の単体テストが含まれています。  
  
-   SQL Server オブジェクト エクスプローラーで開いているプロジェクトのストアド プロシージャ、関数、またはトリガーから単体テストを作成する。 単体テストを作成するときに、指定した場合は SQL Server Data Tools によってテスト プロジェクトも作成されます。 このプロジェクトには、SQL Server 単体テスト クラスが含まれています。 SQL Server 単体テスト クラスには、1 つ以上の単体テストが含まれています。  
  
それぞれの方法については、次の手順で説明します。  
  
### <a name="to-add-a-test-project-to-an-existing-solution"></a>既存のソリューションにテスト プロジェクトを追加するには  
  
1.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  **[インストールされたテンプレート]** で、 **[SQL Server]** ノードを展開し、 **[SQL Server データベース プロジェクト]** を選択します。  
  
3.  **[名前]** ボックスにプロジェクトの名前を入力します。  
  
### <a name="to-create-a-test-project-with-a-sql-server-unit-test-class"></a>SQL Server の単体テスト クラスを使用してテスト プロジェクトを作成するには  
  
-   「[空の SQL Server の単体テストを作成する方法](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)」または「[関数、トリガー、およびストアド プロシージャに対する SQL Server の単体テストを作成する方法](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)」で説明されている手順に従ってください。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
