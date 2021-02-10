---
description: OLE DB プロバイダー (ADO)
title: OLE DB プロバイダー (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e70762a2cbaa6e2dd3d8d91b824591799605748
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032664"
---
# <a name="ole-db-providers-ado"></a>OLE DB プロバイダー (ADO)
OLE DB は、さまざまな情報ソースに格納されているデータへの一貫したアクセスをアプリケーションに提供する一連の COM インターフェイスを定義します。 この方法を使用すると、データソースは、データソースに適した DBMS 機能の量をサポートするインターフェイスを介してデータを共有できます。 設計上、OLE DB の高パフォーマンスアーキテクチャは、柔軟なコンポーネントベースのサービスモデルを使用することに基づいています。 OLE DB は、アプリケーションとデータの間に指定された数の中間層を用意するのではなく、特定のタスクを実行するために必要な数のコンポーネントのみを必要とします。  
  
 たとえば、ユーザーがクエリを実行したいとします。 以下のようなシナリオが考えられます。  
  
-   データは、現在 ODBC ドライバーが存在していて、ネイティブ OLE DB プロバイダーが存在しないリレーショナルデータベースに存在します。このアプリケーションでは、ADO を使用して OLE DB Provider for ODBC と対話し、適切な ODBC ドライバーを読み込みます。 ドライバーは SQL ステートメントを DBMS に渡し、データを取得します。  
  
-   データは、ネイティブ OLE DB プロバイダーが存在する Microsoft SQL Server に存在します。アプリケーションは、ADO を使用して Microsoft SQL Server の OLE DB プロバイダーと直接やり取りします。 中継局は必要ありません。  
  
-   このデータは Microsoft Exchange Server に存在し、SQL クエリを処理するエンジンを公開しない OLE DB プロバイダーが存在します。このアプリケーションでは、ADO を使用して Microsoft Exchange の OLE DB プロバイダーと対話し、クエリを処理するために OLE DB クエリプロセッサコンポーネントに対してを呼び出します。  
  
-   このデータは、Microsoft NTFS ファイルシステムのドキュメント形式で格納されます。データには、Microsoft Indexing Service 経由でネイティブ OLE DB プロバイダーを使用してアクセスします。これにより、ファイルシステム内のドキュメントのコンテンツとプロパティのインデックスが作成され、効率的なコンテンツ検索が可能になります。  
  
 上記のすべての例では、アプリケーションはデータに対してクエリを実行できます。 ユーザーのニーズは、最小数のコンポーネントで満たされています。 いずれの場合も、必要に応じて追加のコンポーネントが使用され、必要なコンポーネントのみが呼び出されます。 OLE DB を使用すると、再利用可能な共有可能なコンポーネントのオンデマンド読み込みが、高パフォーマンスに大きく影響します。  
  
 プロバイダーは、データを提供するカテゴリとサービスを提供するカテゴリの2つのカテゴリに分類されます。 データプロバイダーは独自のデータを所有し、アプリケーションに表形式で公開します。 サービスプロバイダーは、データを生成して使用することによってサービスをカプセル化し、ADO アプリケーションの機能を強化します。 サービスプロバイダーは、他のサービスプロバイダーまたはコンポーネントと連携して動作する必要があるサービスコンポーネントとしてさらに定義することもできます。  
  
 ADO は、さまざまな OLE DB プロバイダーに対して一貫した、より高度なインターフェイスを提供します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [データ プロバイダー](./data-providers.md)  
  
-   [サービス プロバイダーとコンポーネント](./service-providers-and-components.md)