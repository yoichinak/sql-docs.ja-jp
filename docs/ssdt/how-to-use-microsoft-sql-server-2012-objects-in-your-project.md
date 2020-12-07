---
title: プロジェクトの SQL Server 2012 オブジェクト
description: SQL Server 2012 シーケンスについて理解します。 これらのオブジェクトをデータベース プロジェクトに追加して、クエリで使用する方法について説明します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9baf122f-cf22-4860-98db-ef782cd972fc
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: ee09f89463151f0dcf5c1fcd2c1f82a72ba8f350
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988188"
---
# <a name="how-to-use-microsoft-sql-server-2012-objects-in-your-project"></a>方法:プロジェクトで Microsoft SQL Server 2012 のオブジェクトを使用する

この例では、Microsoft SQL Server 2012 をターゲットとするデータベース プロジェクトに、シーケンス オブジェクトを追加します。  
  
シーケンスは、Microsoft SQL Server 2012 で導入されたものです。 シーケンスは、シーケンスが作成された仕様に従って数値のシーケンスを生成するユーザー定義のスキーマ バインド オブジェクトです。 数値のシーケンスは、定義された間隔で昇順または降順に生成され、要求に応じて繰り返されます。  シーケンス オブジェクトについて詳しくは、「[シーケンス番号](../relational-databases/sequence-numbers/sequence-numbers.md)」をご覧ください。 Microsoft SQL Server 2012 の新機能に関する情報は、「[SQL Server 2012 における新機能」](/previous-versions/sql/sql-server-2012/bb500435(v=sql.110))」をご覧ください。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」および「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-add-a-new-sequence-object-to-your-project"></a>新しいシーケンス オブジェクトをプロジェクトに追加するには  
  
1.  **ソリューション エクスプローラー**で **TradeDev** データベース プロジェクトを右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。  
  
2.  左ペインの **[プログラミング]** をクリックし、 **[シーケンス]** をクリックします。 **[追加]** をクリックして新しいオブジェクトをプロジェクトに追加します。  
  
3.  既定のコードを以下で置き換えます。  
  
    ```  
    CREATE SEQUENCE [dbo].[Seq1]  
    AS INT  
    START WITH 1  
    INCREMENT BY 1  
    MAXVALUE 1000  
    NO CYCLE  
    CACHE 10  
    ```  
  
4.  プロジェクトのターゲット プラットフォームが Microsoft SQL Server 2012 に設定されていない場合は、`CREATE SEQUENCE` ステートメントに対する構文エラーが **[エラー一覧]** に表示されます。 これを修正するには、「[ターゲット プラットフォームを変更し、データベース プロジェクトを公開する方法](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)」の手順に従ってターゲット プラットフォームを変更します。  
  
5.  「[ターゲット プラットフォームを変更し、データベース プロジェクトを公開する方法](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)」の手順に従って、接続された Microsoft SQL Server 2012 サーバーにあるデータベースにプロジェクトを公開します。  
  
### <a name="to-use-the-new-sequence-object"></a>新しいシーケンス オブジェクトを使用するには  
  
1.  SQL Server オブジェクト エクスプローラーで、前の手順で公開したデータベースを右クリックし、 **[新しいクエリ]** をクリックします。  
  
2.  次のコードをクエリ ウィンドウに貼り付けます。  
  
    ```  
    DECLARE @counter INT  
    SET @counter=0  
    WHILE @counter<10  
    BEGIN  
        SET @counter = @counter +1  
         INSERT dbo.Products (Id, Name, CustomerId) VALUES (NEXT VALUE FOR dbo.Seq1, 'ProductItem'+cast(@counter as varchar), 1)  
    END   
    GO  
    ```  
  
3.  **[クエリの実行]** をクリックします。  
  
4.  **SQL Server オブジェクト エクスプローラー**で、データベース内の **Products** テーブルに移動します。 右クリックして **[データの表示]** をクリックし、新しく追加された行を確認します。  
