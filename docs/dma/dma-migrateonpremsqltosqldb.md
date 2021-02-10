---
title: Data Migration Assistant を使用して SQL Server を Azure SQL Database に移行する
description: Data Migration Assistant を使用して、オンプレミスの SQL Server をに移行する方法について説明し Azure SQL Database
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 7bd846f4c4abd2a6b9fbcdc434964b789f32d047
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100030640"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>Data Migration Assistant を使用して、オンプレミスの SQL Server または Azure Vm の SQL Server を Azure SQL Database に移行する

Data Migration Assistant は、オンプレミスの SQL Server と、それ以降のバージョンの SQL Server へのアップグレード、または Azure Vm または Azure SQL Database での SQL Server への移行をシームレスに評価します。

この記事では、Data Migration Assistant を使用してオンプレミス SQL Server を Azure SQL Database に移行する手順について説明します。

## <a name="create-a-new-migration-project"></a>新しい移行プロジェクトを作成する

1. 左側のウィンドウで、[ **新規** ] (+) を選択し、 **移行** プロジェクトの種類を選択します。

2. [ソースの種類] を [ **SQL Server** ] に設定し、対象サーバーの種類を [ **Azure SQL Database**] に設定します。

3. **［作成］** を選択します

   ![移行プロジェクトの作成](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>ソース サーバーとデータベースの指定

1. [ソース] の [ソース **サーバーへの接続**] で、[ **サーバー名** ] テキストボックスにソース SQL Server インスタンスの名前を入力します。

2. ソース SQL Server インスタンスによってサポートされる **[認証の種類]** を選択します。

   > [!NOTE]
   > 接続を暗号化する場合は、[接続] の下にある [ **暗号化接続** ] チェックボックスをオンにすることをお **勧めします**。

    ![ソースサーバーの選択](../dma/media/select-source-server.png)

3. **[接続]** を選択します。

4. Azure SQL Database に移行する1つのソースデータベースを選択します。

   > [!NOTE]
   > 移行前にデータベースを評価し、推奨される修正プログラムを表示して適用する場合は、[ **移行前にデータベースを評価** する] チェックボックスをオンにします。

    ![ソースデータベースの選択](../dma/media/select-source-database.png)

5. **[次へ]** を選択します。

## <a name="specify-the-target-server-and-database"></a>ターゲット サーバーとデータベースの指定

1. ターゲットについては、[ **接続先のサーバーへの接続**] の [ **サーバー名** ] ボックスに、Azure SQL Database インスタンスの名前を入力します。 

2. ターゲット Azure SQL Database インスタンスでサポートされている **認証の種類** を選択します。

   > [!NOTE]
   > 接続を暗号化する場合は、[接続] の下にある [ **暗号化接続** ] チェックボックスをオンにすることをお **勧めします**。

     ![対象サーバーの選択](../dma/media/select-target-server.png)

3. **[接続]** を選択します。

4. 移行先の単一の対象になるデータベースを選択します。

   > [!NOTE]
   > Windows ユーザーを移行する場合は、[ **ターゲットの外部ユーザーのドメイン名** ] テキストボックスで、ターゲットの外部ユーザーのドメイン名が正しく指定されていることを確認します。

    ![ターゲットデータベースの選択](../dma/media/select-target-database.png)

5. **[次へ]** を選択します。

## <a name="select-schema-objects"></a>スキーマ オブジェクトの選択

1. Azure SQL Database に移行するソース データベースからスキーマ オブジェクトを選択します。

    ![スキーマ オブジェクトの選択](../dma/media/select-schema-objects.png)

    > [!NOTE]
    > そのまま変換できないオブジェクトの一部が、自動修正の可能性と共に表示されます。 左側のウィンドウでこれらのオブジェクトをクリックすると、右側のウィンドウに提案された修正が表示されます。 修正を確認して、オブジェクトごとにすべての変更を適用するか、無視するかを選びます。 1 つのオブジェクトに対してすべての変更を適用するか、無視しても、他のデータベース オブジェクトには変更が適用されないことに注意してください。 変換できない、または自動修正できないというステートメントが、対象になるデータベースに対して再現され、コメントされます。

    ![修正案](../dma/media/suggested-fix.png)

2. [ **全般] [SQL スクリプト**] を選択します。

3. 生成されたスクリプトを確認します。

    ![生成されたスクリプト](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>スキーマの配置

1. [ **スキーマの配置**] を選択します。

2. スキーマの配置の結果を確認します。

    ![スキーマの配置結果](../dma/media/schema-deployment-results.png)

3. データ移行プロセスを開始するには、[ **データの移行** ] を選択します。

4. 移行するデータを含むテーブルを選択します。

    ![移行するテーブルの選択](../dma/media/select-tables-to-migrate.png) 

5. [ **データ移行の開始**] を選択します。

最後の画面に全体的な状態が表示されます。

   ![移行の状態](../dma/media/migration-status.png) 

## <a name="see-also"></a>関連項目

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Data Migration Assistant: 構成設定](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: ベストプラクティス](../dma/dma-bestpractices.md)
