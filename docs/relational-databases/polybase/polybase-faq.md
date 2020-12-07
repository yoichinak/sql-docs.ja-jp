---
title: PolyBase のよく寄せられる質問 |Microsoft Docs
description: PolyBase とリンク サーバーを比較して、ビッグ データ クラスターの PolyBase とスタンドアロン インスタンスの PolyBase を比較します。 PolyBase 2019 の新機能について説明します。
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.openlocfilehash: 627afe62630dbca81c77bef45d8263824d8c41df
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "96127852"
---
# <a name="frequently-asked-questions"></a>よく寄せられる質問

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="polybase-vs-linked-servers"></a>PolyBase と リンク サーバー
次の表に、PolyBase とリンク サーバーの機能の違いを示します。

|PolyBase | リンク サーバー|
|--------------------------|--------------------------|  
|データベース スコープ オブジェクト|インスタンス スコープ オブジェクト|
|ODBC ドライバーを使用します|OLEDB プロバイダーを使用します|
|すべてのデータ ソースに対して読み取り専用操作をサポートし、HADOOP およびデータ プールのデータ ソースに対してのみ挿入操作をサポートします|読み取りと書き込み両方の操作をサポートします|
|単一の接続からのリモート データ ソースに対するクエリをスケールアウトできます |単一の接続からのリモート データ ソースに対するクエリをスケールアウトできません|
|述語のプッシュダウンがサポートされています|述語のプッシュダウンがサポートされています|
|可用性グループについて個別に構成する必要はありません|可用性グループの各インスタンスについて個別に構成する必要があります|
|基本認証のみ|基本認証と統合認証|
|多くの行を処理する分析クエリに適しています|1 つまたは少数の行を返す OLTP クエリに適しています|
|外部テーブルを使用するクエリは分散トランザクションに参加できません|分散クエリが分散トランザクションに参加できます|

## <a name="whats-new-in-polybase-2019"></a>PolyBase 2019 の新機能 

[!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] の PolyBase は、さまざまな大規模なデータ ソースからデータを読み取ることができるようになりました。 これらの外部データ ソースのデータは、SQL Server で外部テーブルとして格納できます。 PolyBase により、ODBC ジェネリック型を除くこれらの外部データ ソースへのプッシュ ダウン計算もサポートされます。

### <a name="compatible-data-sources"></a>互換性のあるデータ ソース

- SQL Server
- Oracle
- Teradata
- MongoDB
- 互換性のある ODBC ジェネリック型
  
> [!NOTE]
> PolyBase では、サード パーティ製 ODBC ドライバーを使用して外部データ ソースへの接続を許可できます。 これらのドライバーは PolyBase と共に提供されておらず、意図したとおりに動作しない可能性があります。 詳しくは、PolyBase ODBC ジェネリック構成に関する[ガイド](../../relational-databases/polybase/polybase-configure-odbc-generic.md)をご覧ください。  

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>ビッグ データ クラスターの PolyBase とスタンドアロン インスタンスの PolyBase

次の表では、[!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] のスタンドアロン インストールと [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] のビッグ データ クラスターで使用できる PolyBase の機能について説明します。

|機能 |ビッグ データ クラスター|スタンドアロン インスタンス|
|--------------------------|--------------------------|---------|   
|SQL Server、Oracle、Teradata、Mongo DB に対する外部データ ソースを作成する |X|X |
|互換性のあるサードパーティ製 ODBC ドライバーを使用して外部データ ソースを作成する | | X|
|HADOOP データ ソースに対する外部データ ソースを作成する | X| X|
|Azure Blob Storage に対する外部データ ソースを作成する | X| X|
|SQL Server データ プールに外部テーブルを作成する | X| |
|SQL Server ストレージ プールに外部テーブルを作成する | X| |
|クエリの実行をスケールアウトする | X| X|

> [!NOTE]
>この表では、最新の [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] CTP で利用できる機能については説明されていません。 使用可能な機能については、リリース ノートをご覧ください。 ODBC ジェネリック コネクタを使用した接続の詳細については、[ODBC ジェネリック型を構成するためのハウツー ガイド](polybase-configure-odbc-generic.md)の記事をご覧ください。