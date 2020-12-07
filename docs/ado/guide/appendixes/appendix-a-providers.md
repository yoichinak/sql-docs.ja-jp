---
description: '付録 A: データおよびサービスプロバイダー'
title: '付録 A: Providers |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: rothja
ms.author: jroth
ms.openlocfilehash: d50f77959b21031b03ae9591181c61a3419577fd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991173"
---
# <a name="appendix-a-data-and-service-providers"></a>付録 A: データおよびサービスプロバイダー
このセクションでは、データプロバイダー、サービスプロバイダー、およびサービスコンポーネントの3種類のプロバイダーについて説明します。 プロバイダーは、データを提供するカテゴリとサービスを提供するカテゴリの2つのカテゴリに分類されます。 *データプロバイダー*は独自のデータを所有し、アプリケーションに表形式で公開します。 *サービスプロバイダー*は、データを生成して使用することによってサービスをカプセル化し、ADO アプリケーションの機能を強化します。 サービスプロバイダーは、他のサービスプロバイダーまたはコンポーネントと連携して動作する必要がある *サービスコンポーネント*としてさらに定義することもできます。

## <a name="data-providers"></a>データ プロバイダー
 ADO は、さまざまなデータプロバイダーのいずれかに接続でき、特定のプロバイダーの特定の機能に関係なく同じプログラミングモデルを公開できるため、強力で柔軟性があります。

 ただし、各データプロバイダーは一意であるため、アプリケーションと ADO の対話方法はデータプロバイダーによって多少異なります。 これらの違いは、通常、次の3つのカテゴリのいずれかに分類されます。

-   [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)プロパティの接続パラメーター。

-   [コマンド](../../reference/ado-api/command-object-ado.md) オブジェクトの使用法。

-   プロバイダー固有の [レコードセット](../../reference/ado-api/recordset-object-ado.md) の動作。

 Microsoft から現在提供されている各データプロバイダーの詳細については、次の一覧を参照してください。

|領域|トピック|
|----------|-----------|
|ODBC データベース|[Microsoft OLE DB Provider for ODBC](./microsoft-ole-db-provider-for-odbc.md)|
|Microsoft インデックスサービス|[Microsoft OLE DB Provider for Microsoft Indexing Service](./microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory サービス|[Microsoft OLE DB Provider for Microsoft Active Directory サービス](./microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet データベース|[Microsoft Jet 用 OLE DB プロバイダー](./microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB Provider for SQL Server](./microsoft-ole-db-provider-for-sql-server.md)|
|Oracle データベース|[Microsoft OLE DB Provider for Oracle](./microsoft-ole-db-provider-for-oracle.md)|
|インターネット公開|[Microsoft OLE DB Provider for Internet Publishing](./microsoft-ole-db-provider-for-internet-publishing.md)|
|単純なデータソース|[Microsoft OLE DB Simple プロバイダー](./microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>プロバイダー固有の動的プロパティ
 [Connection](../../reference/ado-api/connection-object-ado.md)、 [Command](../../reference/ado-api/command-object-ado.md)、および[Recordset](../../reference/ado-api/recordset-object-ado.md)オブジェクトの[properties](../../reference/ado-api/properties-collection-ado.md)コレクションには、プロバイダー固有の動的プロパティが含まれます。 これらのプロパティは、ADO がサポートする組み込みプロパティ以外のプロバイダー固有の機能に関する情報を提供します。

 接続を確立し、これらのオブジェクトを作成したら、オブジェクトの**properties**コレクションに対して[Refresh](../../reference/ado-api/refresh-method-ado.md)メソッドを使用して、プロバイダー固有のプロパティを取得します。 これらの動的プロパティの詳細については、プロバイダーのドキュメントと [OLE DB プログラマーガイド](/previous-versions/windows/desktop/ms713643(v=vs.85)) を参照してください。

## <a name="service-providers"></a>サービス プロバイダー
 サービスプロバイダーを使用するには、キーワードを指定する必要があります。 また、各サービスプロバイダーに関連付けられているプロバイダー固有の動的プロパティにも注意する必要があります。 プロバイダー固有の詳細については、Microsoft から現在提供されているサービスプロバイダーごとに記載されています。

-   [Microsoft Data Shaping Service for OLE DB](./microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB 永続化プロバイダー](./microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB リモート処理プロバイダー](./microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>サービス コンポーネント
 OLE DB サービスコンポーネント [用の Cursor service](./microsoft-cursor-service-for-ole-db-ado-service-component.md) は、データプロバイダーのカーソルサポート機能を補完します。 また、キーワードと動的プロパティが必要です。

 OLE DB プロバイダーの詳細については、「 [Microsoft OLE DB](/previous-versions/windows/desktop/ms722784(v=vs.85))」を参照してください。

## <a name="provider-commands"></a>プロバイダーコマンド
 ここに一覧表示されているプロバイダーごとに、アプリケーションでプロバイダーコマンドとして SQL ステートメントを入力できるようにするには、ユーザー入力を常に検証する必要があり `DROP TABLE t1` ます。また、ユーザー入力の一部として、などの危険な sql ステートメントを使用してハッカー攻撃を受ける可能性があります。

## <a name="see-also"></a>参照
 [コマンドオブジェクト (ado)](../../reference/ado-api/command-object-ado.md) [接続オブジェクト (ado)](../../reference/ado-api/connection-object-ado.md) Microsoft [OLE DB provider For Internet Publishing](./microsoft-ole-db-provider-for-internet-publishing.md) Microsoft [OLE DB Provider for microsoft Active Directory Service](./microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [microsoft OLE DB PROVIDER for microsoft インデックスサービス](./microsoft-ole-db-provider-for-microsoft-indexing-service.md)Microsoft OLE DB provider For [ODBC](./microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB Provider for Oracle](./microsoft-ole-db-provider-for-oracle.md) microsoft OLE DB provider For [MICROSOFT Jet](./microsoft-ole-db-provider-for-microsoft-jet.md) [Properties Collection (](../../reference/ado-api/properties-collection-ado.md) ado) [Recordset Object (](../../reference/ado-api/recordset-object-ado.md) ado) [Refresh Method (RDS)](../../reference/rds-api/refresh-method-rds.md) [を実行](./microsoft-ole-db-provider-for-sql-server.md)します。