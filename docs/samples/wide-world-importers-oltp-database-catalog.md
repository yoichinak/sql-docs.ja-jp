---
title: WideWorldImporters OLTP データベースカタログ-SQL |Microsoft Docs
description: WideWorldImporters サンプルデータベースカタログのスキーマ、テーブル、ストアドプロシージャ、および設計に関する考慮事項について説明します。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 991f001ea8fd43298cefe1f9ba542472de6935ef
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100354092"
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters データベースカタログ
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
WideWorldImporters データベースには、販売および購入のためのすべてのトランザクション情報と毎日のデータのほか、車両やコールドルームのセンサーデータも含まれています。

## <a name="schemas"></a>スキーマ

WideWorldImporters は、データの格納、ユーザーがデータにアクセスする方法の定義、データウェアハウスの開発と統合のためのオブジェクトの提供など、さまざまな目的にスキーマを使用します。

### <a name="data-schemas"></a>データ スキーマ

これらのスキーマにはデータが含まれています。 他のすべてのスキーマでは、複数のテーブルが必要であり、アプリケーションスキーマに格納されています。

|スキーマ|説明|
|-----------------------------|---------------------|
|Application|アプリケーション全体のユーザー、連絡先、およびパラメーター。 これには、複数のスキーマで使用されるデータを含む参照テーブルも含まれます。|
|購入|サプライヤーからの在庫品目の購入とサプライヤーに関する詳細。|  
|売上|小売顧客に対する在庫品目の売上、および顧客と販売員に関する詳細。 |  
|Warehouse|在庫品目の在庫とトランザクション。|  

### <a name="secure-access-schemas"></a>セキュリティで保護されたアクセススキーマ

これらのスキーマは、データテーブルへの直接アクセスが許可されていない外部アプリケーションに使用されます。 外部アプリケーションで使用されるビューとストアドプロシージャが含まれています。

|スキーマ|説明|
|-----------------------------|---------------------|
|Web サイト|会社の web サイトからデータベースへのすべてのアクセスは、このスキーマを通じて行われます。|
|Reports|Reporting Services レポートからデータベースへのすべてのアクセスは、このスキーマを介して行われます。|
|PowerBI|エンタープライズゲートウェイ経由の Power BI ダッシュボードからデータベースへのすべてのアクセスは、このスキーマを介して行われます。|

レポートおよび PowerBI スキーマは、サンプルデータベースの初期リリースでは使用されないことに注意してください。 ただし、このデータベース上に構築されたすべての Reporting Services と Power BI のサンプルには、これらのスキーマを使用することをお勧めします。

### <a name="development-schemas"></a>開発スキーマ

特別な用途のスキーマ

|スキーマ|説明|
|-----------------------------|---------------------|
|統合|データウェアハウスの統合に必要なオブジェクトとプロシージャ (つまり、データを WideWorldImportersDW データベースに移行する)。|
|シーケンス|アプリケーション内のすべてのテーブルによって使用されるシーケンスを保持します。|

## <a name="tables"></a>テーブル

データベース内のすべてのテーブルがデータスキーマに含まれています。

### <a name="application-schema"></a>アプリケーションスキーマ

共通の参照テーブル (複数の他のスキーマに共通) と共に、パラメーターとユーザー (ユーザーと連絡先) の詳細。

|テーブル|説明|
|-----------------------------|---------------------|
|SystemParameters|システム全体の構成可能なパラメーターを格納します。|
|ユーザー|アプリケーションを使用するすべてのユーザー名、連絡先情報、およびユーザーの組織で大規模なインポーターが処理を行うユーザーについて説明します。 これには、スタッフ、顧客、仕入先、およびその他の連絡先が含まれます。 システムまたは web サイトを使用するためのアクセス許可が付与されているユーザーについては、ログインの詳細が含まれます。|
|市区町村|システムには多くの住所が格納されており、ユーザー、顧客組織の配送先住所、サプライヤーの集配住所などがあります。アドレスが格納されている場合は、このテーブルに市区町村への参照があります。 また、都市ごとに空間の場所もあります。|
|StateProvinces|都市は州または都道府県の一部です。 このテーブルには、各都道府県の境界を示す空間データなどの詳細が含まれています。|
|国|都道府県は国の一部です。 このテーブルには、各国の境界を示す空間データなど、これらの詳細が含まれています。|
|DeliveryMethods|在庫品目の配送の選択肢 (トラック/van、投稿、集配、媒体使用など)|
|PaymentMethods|支払いを行うための選択肢 (例: 現金、小切手、EFT など)|
|TransactionTypes|顧客、仕入先、または在庫取引 (請求書、クレジットメモなど) の種類|

### <a name="purchasing-schema"></a>購入スキーマ

サプライヤーおよび在庫品目の購入の詳細。

|テーブル|説明|
|-----------------------------|---------------------|
|Suppliers (仕入先)|仕入先 (組織) のメインエンティティテーブル|
|SupplierCategories|仕入先のカテゴリ (例: novelties、toys、衣料、パッケージングなど)|
|SupplierTransactions|仕入先に関連するすべての金融取引 (請求書、支払い)|
|Purchaseorders.xaml|仕入先の注文書の詳細|
|PurchaseOrderLines|仕入先の注文書からの詳細行|

 
### <a name="sales-schema"></a>売上スキーマ

顧客、販売員、在庫品目の売上の詳細。

|テーブル|説明|
|-----------------------------|---------------------|
|顧客|顧客 (組織または個人) のメインエンティティテーブル|
|顧客のカテゴリ|顧客向けのカテゴリ (ie 分野ストア、supermarkets など)|
|BuyingGroups|お客様の組織は、より大きな購入力を持つグループに属している場合があります|
|顧客トランザクション|顧客関連のすべての金融取引 (請求書、支払い)|
|特別取引|特別価格。 これには、固定価格、割引 (ドル単位または割引率) を含めることができます。|
|Orders|顧客の注文の詳細|
|OrderLines|顧客の注文の詳細行|
|Invoices|顧客の請求書の詳細|
|InvoiceLines|顧客の請求書の詳細行|

### <a name="warehouse-schema"></a>ウェアハウススキーマ

在庫品目、その所有者、およびトランザクションの詳細。

|テーブル|説明|
|-----------------------------|---------------------|
|StockItems|在庫品目のメインエンティティテーブル|
|StockItemHoldings|在庫品目の非テンポラル列。 これらは頻繁に更新される列です。|
|StockGroups|在庫品目を分類するためのグループ (例: novelties、toys、edible など)|
|StockItemStockGroups|どの在庫品目が在庫グループに含まれているか (多対多)|
|色|ストック項目には色を含めることができます (オプション)|
|PackageTypes|在庫品目をパッケージ化する方法 (箱、容器、パレット、kg など)。|
|StockItemTransactions|すべての在庫品目のすべての移動をカバーするトランザクション (領収、販売、損金処理)|
|VehicleTemperatures|車両冷却装置の温度を定期的に記録|
|すべての温度|コールドルーム冷却装置の温度を定期的に記録する|


## <a name="design-considerations"></a>設計上の考慮事項

データベースの設計は主観的であり、データベースを設計するための適切な方法や不正確な方法はありません。 このデータベースのスキーマとテーブルには、独自のデータベースを設計するためのアイデアが示されています。

### <a name="schema-design"></a>スキーマの設計

WideWorldImporters は少数のスキーマを使用するため、データベースシステムを理解しやすく、データベースの原則を示すことができます。  

可能な限り、データベースは、結合の複雑さを最小限に抑えるために、よくクエリされるテーブルを同じスキーマに併置します。

データベーススキーマは、別のデータベース WWI_Preparation 内の一連のメタデータテーブルに基づいてコード生成されています。 これにより、設計の一貫性、名前の一貫性、および完全性の WideWorldImporters が非常に高くなります。 スキーマが生成された方法の詳細については、次のソースコードを参照してください: [wwi](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>テーブル設計

- 結合を簡単にするために、すべてのテーブルに単一列の主キーがあります。
- すべてのスキーマ、テーブル、列、インデックス、および check 制約には、オブジェクトまたは列の目的を特定するために使用できる Description 拡張プロパティがあります。 メモリ最適化テーブルは、現在拡張プロパティをサポートしていないため、この例外が発生します。
- すべての外部キーは、同じ左側のコンポーネントを持つ別の非クラスター化インデックスが存在しない限り、自動的にインデックスが作成されます。
- テーブルの自動番号付けは、シーケンスに基づいています。 これらのシーケンスは、ID 列とは異なり、リンクサーバーや同様の環境で使用する方が簡単です。 メモリ最適化テーブルは、SQL Server 2016 でサポートされていないため、ID 列を使用します。
- これらのテーブルには、次のような1つのシーケンス (TransactionID) が使用されます: 顧客トランザクション、SupplierTransactions、StockItemTransactions。 これは、一連のテーブルが1つのシーケンスを持つことができる方法を示しています。
- 一部の列には、適切な既定値があります。

### <a name="security-schemas"></a>セキュリティスキーマ

セキュリティのため、WideWorldImporters では外部アプリケーションがデータスキーマに直接アクセスすることは許可されていません。 アクセスを分離するために、WideWorldImporters はデータを保持しないが、ビューとストアドプロシージャを含むセキュリティアクセススキーマを使用します。 外部アプリケーションは、セキュリティスキーマを使用して、表示が許可されているデータを取得します。  このようにして、ユーザーは、セキュリティで保護されたアクセススキーマでのみビューとストアドプロシージャを実行できます。

たとえば、このサンプルには Power BI ダッシュボードが含まれています。 外部アプリケーションは、PowerBI スキーマに対する読み取り専用アクセス許可を持つユーザーとして Power BI ゲートウェイからこれらの Power BI ダッシュボードにアクセスします。  読み取り専用アクセス許可の場合、ユーザーに必要なのは、PowerBI スキーマに対する SELECT 権限と EXECUTE 権限だけです。 WWI のデータベース管理者は、必要に応じてこれらのアクセス許可を割り当てます。

## <a name="stored-procedures"></a>ストアド プロシージャ

ストアドプロシージャは、スキーマで構成されます。 ほとんどのスキーマは、構成またはサンプルの目的で使用されます。

スキーマには、 `Website` Web フロントエンドで使用できるストアドプロシージャが含まれています。

`Reports`および `PowerBI` スキーマは、reporting Services と PowerBI の目的で使用されます。 このサンプルの拡張機能には、レポートのためにこれらのスキーマを使用することをお勧めします。

### <a name="website-schema"></a>Web サイトスキーマ

これらは、Web フロントエンドなどのクライアントアプリケーションによって使用される手順です。

|プロシージャ|目的|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|ユーザーが `Application.People` web サイトにアクセスできるようにします。|
|ChangePassword|ユーザーのパスワードを変更します (外部の認証メカニズムを使用していないユーザーの場合)。|
|InsertCustomerOrders|1つまたは複数の顧客の注文 (注文明細を含む) を挿入できます。|
|InvoiceCustomerOrders|請求される注文の一覧を取得し、請求書を処理します。|
|Recordcolの温度|センサーデータリストをテーブル値パラメーター (TVP) として受け取り、そのデータを `Warehouse.ColdRoomTemperatures` テンポラルテーブルに適用します。|
|RecordVehicleTemperature|JSON 配列を受け取り、それを使用してを更新 `Warehouse.VehicleTemperatures` します。|
|SearchForCustomers|名前または名前の一部 (会社名または個人名) を使用して顧客を検索します。|
|SearchForPeople|名前または名前の一部で人間を検索します。|
|SearchForStockItems|名前または名前またはマーケティングのコメントの一部で在庫品目を検索します。|
|SearchForStockItemsByTags|タグで在庫項目を検索します。|
|SearchForSuppliers|名前または名前の一部 (会社名または個人名) で仕入先を検索します。|

### <a name="integration-schema"></a>統合スキーマ

このスキーマ内のストアドプロシージャは、ETL プロセスによって使用されます。 これらは、 [ETL パッケージ](wide-world-importers-perform-etl.md)で必要とされる時間帯に、さまざまなテーブルから必要なデータを取得します。

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation スキーマ

売上と購入を挿入するワークロードをシミュレートします。 メインのストアドプロシージャはです `PopulateDataToCurrentDate` 。これは、現在の日付までサンプルデータを挿入するために使用されます。

|プロシージャ|目的|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|データのロードシミュレーションに必要な手順を再作成します。 これは、現在の日付にデータを取り込むために必要です。|
|Configuration_RemoveDataLoadSimulationProcedures|これにより、データシミュレーションが完了した後に、プロシージャが再度削除されます。|
|DeactivateTemporalTablesBeforeDataLoad|すべてのテンポラルテーブルの一時的な性質を削除し、必要に応じてトリガーを適用して、sys-テンポラルテーブルが許可するよりも前の日付で変更を適用できるようにします。|
|PopulateDataToCurrentDate|データを現在の日付まで取り込むために使用されます。 は、最初のバックアップからデータベースを復元した後、他の構成オプションの前に実行する必要があります。|
|ReactivateTemporalTablesAfterDataLoad|データの一貫性のチェックを含む、テンポラルテーブルを再確立します。 (関連付けられているトリガーを削除します)。|


### <a name="application-schema"></a>アプリケーションスキーマ

これらの手順は、サンプルを構成するために使用されます。 これらは、enterprise edition の機能を standard edition バージョンのサンプルに適用し、監査とフルテキストインデックス作成を追加するために使用されます。

|プロシージャ|目的|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|メンバーがロールにまだ存在しない場合は、メンバーをロールに追加します。|
|Configuration_ApplyAuditing|監査を追加します。 サーバー監査は standard edition データベースに適用されます。enterprise edition では、追加のデータベース監査が追加されています。|
|Configuration_ApplyColumnstoreIndexing|列ストアインデックスをに適用し、適切にインデックスを再作成し `Sales.OrderLines` `Sales.InvoiceLines` ます。|
|Configuration_ApplyFullTextIndexing|、、、およびにフルテキストインデックスを適用し `Application.People` `Sales.Customers` `Purchasing.Suppliers` `Warehouse.StockItems` ます。 `Website.SearchForPeople`、、 `Website.SearchForSuppliers` `Website.SearchForCustomers` 、を `Website.SearchForStockItems` 、 `Website.SearchForStockItemsByTags` フルテキストインデックスを使用する置換プロシージャに置き換えます。|
|Configuration_ApplyPartitioning|とにテーブルパーティション分割を適用し、に合わせてインデックスを再配置 `Sales.CustomerTransactions` `Purchasing.SupplierTransactions` します。|
|Configuration_ApplyRowLevelSecurity|販売区域に関連するロールを使って顧客をフィルター処理するために、行レベルのセキュリティを適用します。|
|Configuration_ConfigureForEnterpriseEdition|列ストアインデックス、フルテキスト、メモリ内、polybase、およびパーティション分割を適用します。|
|Configuration_EnableInMemory|メモリ最適化ファイルグループを追加し (Azure で動作していない場合)、を `Warehouse.ColdRoomTemperatures` `Warehouse.VehicleTemperatures` その等価のメモリに置き換え、データを移行します。さらに、、、、、およびメモリ最適化された同等のテーブル型を再作成し、 `Website.OrderIDList` これらの `Website.OrderList` `Website.OrderLineList` `Website.SensorDataList` `Website.InvoiceCustomerOrders` `Website.InsertCustomerOrders` テーブル型を使用するプロシージャを削除して `Website.RecordColdRoomTemperatures` 再作成します。|
|Configuration_RemoveAuditing|監査構成を削除します。|
|Configuration_RemoveRowLevelSecurity|行レベルのセキュリティ構成を削除します (これは、関連付けられているテーブルに対する変更に必要です)。|
|CreateRoleIfNonExistant 存在しません|データベースロールがまだ存在しない場合は、作成します。|


### <a name="sequences-schema"></a>シーケンススキーマ

データベース内のシーケンスを構成する手順。

|プロシージャ|目的|
|-----------------------------|---------------------|
|順序のリセット|すべてのシーケンスに対してプロシージャ ReseedSequenceBeyondTableValue を呼び出します。|
|ReseedSequenceBeyondTableValue|同じシーケンスを使用するテーブルの値を超えて、次のシーケンス値を再配置するために使用されます。 (例として、シーケンスの場合は、複数のテーブル間では、id 列は DBCC CHECKIDENT に相当します)。|
