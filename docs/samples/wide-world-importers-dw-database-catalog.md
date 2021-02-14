---
title: WideWorldImporters OLAP データベースカタログ-SQL |Microsoft Docs
description: WideWorldImportersDW データベースでのデータウェアハウスと分析処理に使用されるスキーマ、テーブル、およびストアドプロシージャについて説明します。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=azuresqldb-mi-current'
ms.openlocfilehash: 4481a0c96a8f4a7f2f82e8babc5d8dce5ea97e92
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100077814"
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW データベースカタログ
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW データベースのスキーマ、テーブル、およびストアドプロシージャについて説明します。 

WideWorldImportersDW データベースは、データウェアハウスと分析処理に使用されます。 販売および購入に関するトランザクションデータは、WideWorldImporters データベースで生成され、 **毎日の ETL プロセス** を使用して WideWorldImportersDW データベースに読み込まれます。

そのため、WideWorldImportersDW 内のデータは WideWorldImporters のデータをミラー化しますが、テーブルの構成は異なります。 WideWorldImporters には従来の正規化されたスキーマがありますが、WideWorldImportersDW では、テーブルの設計に [スタースキーマ](https://wikipedia.org/wiki/Star_schema) のアプローチを使用します。 ファクトテーブルとディメンションテーブル以外にも、ETL プロセスで使用される多数のステージングテーブルがデータベースに含まれています。

## <a name="schemas"></a>スキーマ

さまざまな種類のテーブルは、3つのスキーマで構成されています。

|スキーマ|説明|
|-----------------------------|---------------------|
|Dimension|ディメンションテーブル。|
|ファクト| ファクト テーブル。|  
|統合|ETL に必要なステージングテーブルおよびその他のオブジェクト。|  

## <a name="tables"></a>[テーブル]

ディメンションテーブルとファクトテーブルを以下に示します。 統合スキーマのテーブルは ETL プロセスでのみ使用され、一覧には表示されません。

### <a name="dimension-tables"></a>ディメンション テーブル

WideWorldImportersDW には、次のディメンションテーブルがあります。 説明には、WideWorldImporters データベース内のソーステーブルとのリレーションシップが含まれます。

|テーブル|ソーステーブル|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|Date|財務年度を含む、日付に関する情報を含む新しいテーブル (会計年度の最初の開始日に基づく)。|
|従業員|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|Supplier (仕入先)|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>ファクト テーブル

WideWorldImportersDW には、次のファクトテーブルがあります。 説明には、WideWorldImporters データベース内のソーステーブルとの関係、および各ファクトテーブルが一般的に使用される分析/レポートクエリのクラスが含まれます。

|テーブル|ソーステーブル|サンプル分析|
|-----------------------------|---------------------|---------------------|
|Order|`Sales.Orders` および `Sales.OrderLines`|販売員、ピッカー/packer 生産性、および時間における注文の選択。 さらに、注文のバックにつながる在庫状況が低いという状況もあります。|
|Sale|`Sales.Invoices` および `Sales.InvoiceLines`|販売日、配送日、時間の経過に伴う収益性、営業担当者による収益性。|
|購入|`Purchasing.PurchaseOrderLines`|予想される時間と実際のリードタイム|
|トランザクション|`Sales.CustomerTransactions` および `Purchasing.SupplierTransactions`|発行日と終了日、および金額の測定。|
|移動|`Warehouse.StockTransactions`|時間の経過と共に移動します。|
|在庫保持|`Warehouse.StockItemHoldings`|手持在庫のレベルと価値。|

## <a name="stored-procedures"></a>ストアド プロシージャ

ストアドプロシージャは、主に ETL プロセスと構成の目的で使用されます。

このサンプルの拡張機能には、Reporting Services レポートにスキーマを使用すること `Reports` と、 `PowerBI` power BI アクセス用のスキーマを使用することをお勧めします。

### <a name="application-schema"></a>アプリケーションスキーマ

これらの手順は、サンプルを構成するために使用されます。 これらは、enterprise edition の機能を standard edition バージョンのサンプルに適用し、PolyBase を追加し、ETL を再シードするために使用されます。

|プロシージャ|目的|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|ファクトテーブルのパーティション分割と列ストアインデックスの両方を適用します。|
|Configuration_ConfigureForEnterpriseEdition|パーティション分割、列ストアインデックス作成、およびメモリ内に適用されます。|
|Configuration_EnableInMemory|統合ステージングテーブルを SCHEMA_ONLY メモリ最適化テーブルに置き換えて、ETL のパフォーマンスを向上させます。|
|Configuration_ApplyPolyBase|外部データソース、ファイル形式、およびテーブルを構成します。|
|Configuration_PopulateLargeSaleTable|Enterprise edition の変更を適用した後、2012年のデータ量を追加の履歴として設定します。|
|Configuration_ReseedETL|既存のデータを削除し、ETL シードを再起動します。 これにより、再作成は、OLTP データベースの更新された行と照合することができます。|

### <a name="integration-schema"></a>統合スキーマ

ETL プロセスで使用されるプロシージャは、次のカテゴリに分類されます。
- ETL パッケージのヘルパープロシージャ-すべての Get * プロシージャ。
- ステージングデータを DW テーブルに移行するために ETL パッケージによって使用されるプロシージャ-All Migrate * プロシージャ。
- `PopulateDateDimensionForYear` -年を取り、その年のすべての日付がテーブルに設定されていることを確認し `Dimension.Date` ます。

### <a name="sequences-schema"></a>シーケンススキーマ

データベース内のシーケンスを構成する手順。

|プロシージャ|目的|
|-----------------------------|---------------------|
|順序のリセット|`ReseedSequenceBeyondTableValue`すべてのシーケンスに対してプロシージャを呼び出します。|
|ReseedSequenceBeyondTableValue|同じシーケンスを使用するテーブルの値を超えて、次のシーケンス値を再配置するために使用されます。 ( `DBCC CHECKIDENT` シーケンスに相当する id 列の場合は、複数のテーブルにまたがる場合もあります)。|
