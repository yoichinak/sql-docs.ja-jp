---
title: SQL Server の機能の使用 |Microsoft Docs
description: SQL Server の機能、および WideWorldImporters サンプルデータベースでの使用方法について説明します。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 01/21/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6e20d90d91badcd0961ab03e219bbf6e9a8ae2c8
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100354060"
---
# <a name="use-of-sql-server-features-and-capabilities"></a>SQL Server の機能の使用

[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]

OLTP データベースの SQL Server の機能を WideWorldImporters に使用します。

WideWorldImporters は、SQL Server 2016 で導入された最新機能を含む SQL Server の主な機能の多くを紹介するように設計されています。 次の表に、SQL Server の機能の一覧を示します。 各行には、WideWorldImporters での機能の使用方法についての説明も表示されます。  
&nbsp;

|SQL Server 機能|WideWorldImporters で使用する|
|:-------------------------------|:------------------------|
|テンポラル テーブル|多くのテンポラルテーブルがあります。これには、すべての参照スタイルの参照テーブルと、StockItems、Customers、および業者などの主要なエンティティが含まれます。 テンポラルテーブルを使用すると、これらのエンティティの履歴を追跡しておくことができます。|
|JSON の AJAX 呼び出し|多くの場合、アプリケーションは AJAX 呼び出しを使用してこれらのテーブル (person、Customers、仕入先、および StockItems) に対してクエリを実行します。 この呼び出しは、JSON 形式でデータを返します。 たとえば、ストアドプロシージャを参照してください `Website.SearchForCustomers` 。|
|JSON のプロパティ/値バッグ|多数のテーブルには、テーブル内のリレーショナルデータを拡張するために JSON データを保持する列があります。 たとえば、に `Application.SystemParameters` は、アプリケーション設定の列があり、 `Application.People` ユーザー設定を記録するための列があります。 これらのテーブルは、列を使用し `nvarchar(max)` て json データを記録し、 `ISJSON` 列の値が有効な json であることを保証するために、組み込み関数を使用して check 制約を指定します。|
|行レベルのセキュリティ (RLS)|行レベルセキュリティ (RLS) は、ロールのメンバーシップに基づいて、Customers テーブルへのアクセスを制限するために使用されます。 各販売区域には、ロールとユーザーがあります。 RLS アクセス制限の動作を確認するには、sample-script.zip で対応するスクリプトを使用します。これは、 [サンプルのリリース](https://go.microsoft.com/fwlink/?LinkID=800630)の一部です。|
|リアルタイム運用分析|(完全バージョンのデータベース)コアトランザクションテーブルとには、 `Sales.InvoiceLines` `Sales.OrderLines` 運用ワークロードへの影響を最小限に抑えながら、トランザクションデータベースでの分析クエリの効率的な実行をサポートする非クラスター化列ストアインデックスがあります。 同じデータベースでのトランザクションと分析の実行は、 [ハイブリッドトランザクション/分析処理 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))とも呼ばれます。 この動作を確認するには、 [サンプルのリリース](https://go.microsoft.com/fwlink/?LinkID=800630)の一部である sample-script.zip で対応するスクリプトを使用します。|
|PolyBase|この PolyBase が動作していることを確認するには、Azure ブログストレージでホストされているパブリックデータセットを含む外部テーブルを使用して、sample-script.zip で対応するスクリプトを使用します。これは、 [サンプルのリリース](https://go.microsoft.com/fwlink/?LinkID=800630)の一部です。|
|インメモリ OLTP|(完全バージョンのデータベース)テーブル型はすべてメモリ最適化されているため、テーブル値パラメーター (Tvp) はすべてメモリ最適化の恩恵を受けます。<br/><br/>2つの監視テーブル `Warehouse.VehicleTemperatures` とは、 `Warehouse.ColdRoomTemperatures` メモリ最適化されています。 メモリ最適化を使用すると、従来のディスクベーステーブルよりも高速にテーブルを設定できます。 VehicleTemperatures テーブルは、JSON ペイロードを保持し、IoT シナリオに対する拡張に役立ちます。 VehicleTemperatures テーブルは、EventHubs、Stream Analytics、Power BI に関連するシナリオに対してさらに役立ちます。<br/><br/>このストアドプロシージャ `Website.RecordColdRoomTemperatures` はネイティブにコンパイルされ、コールドルーム温度の記録のパフォーマンスをさらに向上させます。<br/><br/>動作中の OLTP In-Memory の例については、workload-drivers.zip の車両の場所ワークロードドライバーに関するセクションを参照してください。これは、 [サンプルのリリース](https://go.microsoft.com/fwlink/?LinkID=800630)に含まれています。|
|クラスター化列ストア インデックス|(完全バージョンのデータベース)テーブルでは、 `Warehouse.StockItemTransactions` クラスター化列ストアインデックスが使用されます。 このテーブルの行の数は大きくなることが予想され、クラスター化列ストアインデックスはテーブルのディスク上のサイズを大幅に削減し、クエリのパフォーマンスを向上させます。 このテーブルでの変更は挿入のみです。オンラインワークロードでは、このテーブルに対する更新や削除は行われません。クラスター化列ストアインデックスは、挿入ワークロードに適しています。|
|動的なデータ マスキング|データベーススキーマでは、テーブルの仕入先に対して保持されている銀行の詳細にデータマスクが適用されてい `Purchasing.Suppliers` ます。 管理者以外のスタッフは、この情報にアクセスできません。|
|Always Encrypted|Always Encrypted のデモは、 [サンプルのリリース](https://go.microsoft.com/fwlink/?LinkID=800630)の一部であるダウンロード可能な samples.zip に含まれています。 このデモでは、暗号化キー、機密データの暗号化を使用するテーブル、およびテーブルにデータを挿入する小さなサンプルアプリケーションを作成します。|
|Stretch Database|`Warehouse.ColdRoomTemperatures`テーブルはテンポラルテーブルとして実装されており、完全なバージョンのサンプルデータベースでメモリ最適化されています。 アーカイブテーブルはディスクベースであり、Azure に拡張できます。|
|フルテキスト インデックス|フルテキストインデックスを使用すると、ユーザー、顧客、および StockItems の検索が向上します。 インデックスがクエリに適用されるのは、SQL Server インスタンスにフルテキストインデックスがインストールされている場合のみです。 非永続的な計算列は、StockItems テーブルにフルテキストインデックスが作成されているデータを作成するために使用されます。<br/><br/>`CONCAT` は、フルテキストインデックスが作成される SearchData を作成するためにフィールドを連結するために使用されます。<br/>サンプルでフルテキストインデックスを使用できるようにするには、データベースで次のステートメントを実行します。<br/><br/>`EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>既定のフルテキストカタログが存在しない場合は、プロシージャによって作成されます。その後、検索ビューはそれらのビューのフルテキストバージョンに置き換えられます。<br/><br/>SQL Server でフルテキストインデックスを使用するには、インストール時に Full-Text オプションを選択する必要があることに注意してください。 Azure SQL Database では、フルテキストインデックスを有効にするためにおよび特定の構成は必要ありません。|
|インデックス保存された計算列|SupplierTransactions および顧客トランザクションで使用されるインデックス付きの保存済みの計算列。|
|CHECK 制約|比較的複雑な check 制約が `Sales.SpecialDeals` あります。 これにより、DiscountAmount、Discountamount、および UnitPrice の1つだけが構成されます。|
|UNIQUE 制約|に対して多対多の構築 (および unique 制約) が設定されてい `Warehouse.StockItemStockGroups` ます。|
|テーブル パーティション|(完全バージョンのデータベース)テーブル `Sales.CustomerTransactions` とテーブル `Purchasing.SupplierTransactions` は両方とも、パーティション関数とパーティション構成を使用して年でパーティション分割され `PF_TransactionDate` `PS_TransactionDate` ます。 パーティション分割は、大規模なテーブルの管理を向上させるために使用されます。|
|リスト処理|テーブル型の例 `Website.OrderIDList` が用意されています。 これは、例のプロシージャで使用され `Website.InvoiceCustomerOrders` ます。 この手順では、共通テーブル式 (Cte)、TRY/CATCH、JSON_MODIFY、XACT_ABORT、NOCOUNT、THROW、および XACT_STATE を使用して、アプリケーションからデータベースエンジンへのラウンドトリップを最小限に抑えるために、単一の注文ではなく注文の一覧を処理する機能を示します。|
|GZip 圧縮|ビューでは、 `Warehouse.VehicleTemperature` テーブルは全センサーデータを保持します。 しかし、このデータが数か月を超える場合は、領域を節約するために圧縮されます。 COMPRESS 関数は GZip 圧縮を使用します。<br/><br/>ビューでは `Website.VehicleTemperatures` 、以前に圧縮されたデータを取得するときに、圧縮解除機能を使用します。|
|クエリ ストア|データベースでクエリストアが有効になっています。 いくつかのクエリを実行した後、次の手順を実行します。<br/><br/>1. Management Studio でデータベースを開きます。<br/>2. データベースの下にあるノードクエリストアを開きます。<br/>3. [リソースを *消費するクエリの上位*] レポートを開きます。 クエリの実行を確認し、実行したばかりのクエリのプランを確認します。|
|STRING_SPLIT|テーブルの列には `DeliveryInstructions` `Sales.Invoices` 、STRING_SPLIT を示すために使用できるコンマ区切り値があります。|
|Audit|データベースで次のステートメントを実行すると、このサンプルデータベースに対して SQL Server Audit を有効にできます。<br/><br/>`EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>Azure SQL Database では、 [Azure portal](https://portal.azure.com/)によって監査が有効になります。<br/><br/>ログイン、ロール、およびアクセス許可を含むセキュリティ操作は、監査が有効になっているすべてのシステム (standard edition システムを含む) に記録されます。 監査はアプリケーションログに送られます。これは、すべてのシステムで使用できるため、追加のアクセス許可は必要ありません。 セキュリティを強化するために、セキュリティログまたはセキュリティで保護されたフォルダー内のファイルにリダイレクトする必要があることを示す警告が出力されます。 必要な追加構成について説明するリンクが用意されています。<br/><br/>評価/開発者/エンタープライズエディションのシステムでは、すべての財務トランザクションデータへのアクセスが監査されます。|
| &nbsp; | &nbsp; |
