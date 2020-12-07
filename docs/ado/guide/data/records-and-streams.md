---
description: レコードとストリーム
title: レコードとストリーム |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
author: rothja
ms.author: jroth
ms.openlocfilehash: 38bf8e44ec6b9521a1608c6081697295e6d9aedf
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979913"
---
# <a name="records-and-streams"></a>レコードとストリーム
現在、ADO では、リレーショナルデータベースなどのデータソース内の情報にアクセスする主な手段として、 [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md) オブジェクトが提供されています。 ただし、一部のプロバイダーでは、 [レコード](../../../ado/reference/ado-api/record-object-ado.md) オブジェクトおよび [ストリーム](../../../ado/reference/ado-api/stream-object-ado.md) オブジェクトを、プロバイダーからのデータを操作できる代替オブジェクトまたは補完的オブジェクトとしてサポートしています。 **レコード**の動作の詳細については、プロバイダーのドキュメントを参照してください。  
  
## <a name="records"></a>レコード  
 **レコード** オブジェクトは、基本的には1行の **レコードセット**として機能します。 ただし、 **レコード** は、レコード **セット** と比較して機能が制限され、プロパティとメソッドが異なる場合があります。 **レコード** オブジェクト内のデータのソースは、プロバイダーから1行のデータを返すコマンドにすることができます。 レコード**セット**オブジェクトではなく**レコード**オブジェクトを使用して、1行のデータを返すクエリから結果を受け取ると、より複雑な**レコードセット**オブジェクトをインスタンス化するオーバーヘッドがなくなります。  
  
 **レコード** オブジェクトは、特に、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)などの従来のリレーショナルデータベース以外のデータソースのプロバイダーによって、別の目的に利用できます。 処理する必要がある情報の多くは、データベース内のテーブルとしてではなく、電子メールシステムおよび最新のファイルシステムのファイル内のメッセージとして存在します。 **レコード**オブジェクトと**ストリーム**オブジェクトを使用すると、リレーショナルデータベース以外のソースに格納されている情報に簡単にアクセスできます。  
  
 **レコード**オブジェクトは、ファイルシステム内のディレクトリやファイル、電子メールシステム内のフォルダー、メッセージなどのデータを表し、管理できます。 このため、 **レコード** のソースは、開いている **レコードセット**の現在の行、絶対 url、または開いている [接続](../../../ado/reference/ado-api/connection-object-ado.md) オブジェクトと組み合わせた相対 url にすることができます。  
  
 通常、 **レコードセット** を使用して、フォルダーやディレクトリなどの階層内のコンテナーまたは親を表すことができます。 **レコード**を使用して、ファイルやドキュメントなど、親コンテナー内の1つのノードに関する特定の情報を返すことができます。 主な理由 **レコード** は、この種類の情報を表すために使用されます。これは、これらのデータソースが異種であることです。 これは、各 **レコード** のセットとフィールドの数が異なる可能性があることを意味します。 データベースの行を含む従来の **レコードセット** は、同一であり、各行のフィールドの数と型が同じであることを意味します。  
  
 **レコード**オブジェクトを使用して、インターネット発行プロバイダーなどのプロバイダーからのこの異種データを処理する方法の詳細については、「 [Using ADO for internet publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md)」を参照してください。  
  
## <a name="streams"></a>ストリーム  
 **ストリーム**オブジェクトは、バイトのストリームを読み取り、書き込み、および管理するための手段を提供します。 このバイトストリームはテキストまたはバイナリであり、システムリソースによってのみサイズが制限されます。 通常、ADO **Stream** オブジェクトは次の目的で使用されます。  
  
-   XML 形式で保存された **レコードセット** のデータを格納する場合は。 保存された **レコードセット**s からのこれらの XML ストリームは、新しい **レコードセット**を開くときにソースとして使用できます。 詳細については、「 [ストリームと永続](../../../ado/guide/data/streams-and-persistence.md)化」を参照してください。  
  
-   [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)の代替手段としてプロバイダーに対して実行される[commandstreams](../../../ado/reference/ado-api/commandstream-property-ado.md)を格納する場合は。 たとえば、XML アップデートグラムは、Microsoft OLE DB Provider for SQL Server に対するコマンドのソースとして使用できます。  
  
-   Microsoft OLE DB Provider for SQL Server の XML の結果など、 **レコードセット**以外の形式でプロバイダーから結果を受け取る場合は。 詳細については、「 [結果セットをストリームに取得](../../../ado/guide/data/retrieving-resultsets-into-streams.md)する」を参照してください。  
  
-   ファイルまたはメッセージを構成するテキストまたはバイトを格納する場合は。通常は、Microsoft OLE DB Provider for Internet Publishing などのプロバイダーと共に使用します。 この **ストリーム** オブジェクトの使用方法の詳細については、「 [Using ADO for Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md)」を参照してください。  
  
 **ストリーム**オブジェクトは、次のもので開くことができます。  
  
-   URL で指定された単純なファイル。  
  
-   **ストリーム**オブジェクトを含む**レコード**または**レコードセット**のフィールド。  
  
-   ディレクトリまたは複合ファイルを表す **レコード** または **レコードセット** オブジェクトの既定のストリーム。  
  
-   単純ファイルの URL を含むリソースフィールドです。  
  
-   特定のソースがまったくありません。 この場合、 **ストリーム** オブジェクトはメモリで開かれます。 データを書き込んでから別の **ストリーム** またはファイルに保存することができます。  
  
-   **レコードセット**内の BLOB フィールド。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ストリームと永続性](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [コマンド ストリーム](../../../ado/guide/data/command-streams.md)  
  
-   [ストリーム形式で結果セットを取得する](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [インターネットへの発行に ADO を使用する](../../../ado/guide/data/using-ado-for-internet-publishing.md)
