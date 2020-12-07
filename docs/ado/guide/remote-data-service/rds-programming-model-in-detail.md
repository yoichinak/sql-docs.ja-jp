---
description: RDS のプログラミング モデルの詳細
title: RDS プログラミングモデルの詳細 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: rothja
ms.author: jroth
ms.openlocfilehash: a2b307c89d5e4a25d6963ef100083015ffe6ce74
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724923"
---
# <a name="rds-programming-model-in-detail"></a>RDS のプログラミング モデルの詳細
RDS プログラミングモデルの主な要素は次のとおりです。  
  
-   RDS.DataSpace  
  
-   RDSServer DataFactory  
  
-   RDS.DataControl  
  
-   Event  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 クライアントアプリケーションでは、起動するサーバーとサーバープログラムを指定する必要があります。 返されると、アプリケーションはサーバープログラムへの参照を受け取り、その参照をサーバープログラム自体のように扱うことができます。  
  
 RDS オブジェクトモデルは、Rds でこの機能を具体化し [ます。領域スペース](../../reference/rds-api/dataspace-object-rds.md) オブジェクト。  
  
 サーバープログラムには、プログラム識別子 ( *ProgID*) が指定されています。 サーバーは、 *ProgID* とサーバーコンピューターのレジストリを使用して、開始する実際のプログラムに関する情報を検索します。  
  
 RDS は、サーバープログラムがインターネットまたはイントラネット経由のリモートサーバー上にあるかどうかによって、内部的に区別を行います。ローカルエリアネットワーク上のサーバーまたは、サーバー上ではなく、ローカルダイナミックリンクライブラリ (DLL) 上にあります。 この区別によって、クライアントとサーバーの間で情報がどのように交換されるかが決まり、クライアントアプリケーションに返される参照の種類が明確に区別されます。 しかし、視点から見ると、この区別は特別な意味を持ちません。 重要なのは、使用可能なプログラム参照を受け取ることだけです。  
  
## <a name="rdsserverdatafactory"></a>RDSServer DataFactory  
 RDS には、データソースに対して SQL クエリを実行し、 [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトを返すか、 **レコードセット** オブジェクトを取得してデータソースを更新できる既定のサーバープログラムが用意されています。  
  
 RDS オブジェクトモデルは、 [DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) オブジェクトを使用してこの機能を具体化します。  
  
 さらに、このオブジェクトには、プログラムによる入力が可能な空の **レコードセット** オブジェクト ([CreateRecordset](../../reference/rds-api/createrecordset-method-rds.md)) と、 **レコードセット** オブジェクトをテキスト文字列に変換して Web ページを構築するための別の方法 ([converttostring](../../reference/rds-api/converttostring-method-rds.md)) を作成するメソッドがあります。  
  
 ADO では、 **DataFactory**ハンドラーと、接続、コマンド、およびセキュリティの各パラメーターを含むカスタマイズファイルを使用して、 **DataFactory**の標準接続とコマンド動作の一部をオーバーライドできます。  
  
 サーバープログラムは、 *ビジネスオブジェクト*と呼ばれることもあります。 複雑なデータアクセスや有効性チェックなどを実行できる、独自のカスタムビジネスオブジェクトを作成できます。 カスタムビジネスオブジェクトを作成する場合でも、 **RDSServer** オブジェクトのインスタンスを作成し、そのメソッドを使用して独自のタスクを実行することができます。  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS は、Rds の機能を組み合わせる手段を提供し **ます。データ領域と** **RDSServer**を使用すると、データソースのクエリによって返される **レコードセット** オブジェクトをビジュアルコントロールで簡単に使用できるようになります。 RDS は、最も一般的なケースとして、サーバー上の情報へのアクセスを自動的に取得してビジュアルコントロールに表示するために、可能な限り多くのことを試みます。  
  
 RDS オブジェクトモデルは、Rds でこの機能を具体化し [ます。DataControl](../../reference/rds-api/datacontrol-object-rds.md) オブジェクト。  
  
 **RDS。DataControl**には2つの側面があります。 データソースに関連する側面が1つあります。 RDS の **Connect** および **SQL** プロパティを使用して、コマンドと接続情報を設定する場合 **。DataControl**は、RDS を自動的に使用し **ます。** RDSServer を作成して、既定の **DataFactory** オブジェクトへの参照を作成します。 次に、 **RDSServer** は **connect** プロパティ値を使用してデータソースに接続し、 **SQL** プロパティ値を使用してデータソースから **レコードセット** を取得し、 **レコードセット** オブジェクトを RDS に返し **ます。DataControl**。  
  
 2番目の側面は、ビジュアルコントロールで返される **レコードセット** 情報の表示に関連しています。 ビジュアルコントロールを RDS に関連付けることができ **ます。DataControl** (バインディングと呼ばれるプロセス内) で、関連付けられた **レコードセット** オブジェクトの情報にアクセスし、Microsoft® Internet Explorer の Web ページにクエリ結果を表示します。 各 **RDS。DataControl** オブジェクトは、1つのクエリの結果を表す1つの **レコードセット** オブジェクトを1つ以上のビジュアルコントロール (たとえば、テキストボックス、コンボボックス、グリッドコントロールなど) にバインドします。 複数の RDS が存在する場合があり **ます。** 各ページの DataControl オブジェクト。 各 **RDS。DataControl** オブジェクトは、別のデータソースに接続し、別のクエリの結果を含めることができます。  
  
 **RDS。DataControl**オブジェクトには、関連付けられた**レコードセット**オブジェクトの行を移動、並べ替え、およびフィルター処理するための独自のメソッドもあります。 これらのメソッドは似ていますが、ADO **レコードセット** オブジェクトのメソッドと同じではありません。  
  
## <a name="events"></a>events  
 RDS は、ADO イベントモデルに依存しない独自のイベントを2つサポートしています。 [OnReadyStateChange](../../reference/rds-api/onreadystatechange-event-rds.md)イベントは、RDS が呼び出されるたびに呼び出され**ます。DataControl** [ReadyState](../../reference/rds-api/readystate-property-rds.md)プロパティが変更され、非同期操作が正常に完了したか、終了したか、またはエラーが発生したときに通知されます。 [OnError](../../reference/rds-api/onerror-event-rds.md)イベントは、非同期操作中にエラーが発生した場合でも、エラーが発生するたびに呼び出されます。  
  
> [!NOTE]
>  Microsoft Internet Explorer では、RDS に2つの追加イベントを提供しています。 **Ondatasetchanged**。これは、 **レコードセット** が機能していても行を取得し、 **Ondatasetchanged**で、 **レコードセット** が行の取得を完了したことを示します。  
  
## <a name="see-also"></a>参照  
 [オブジェクトを使用した RDS プログラミングモデル](./rds-programming-model-with-objects.md)   
 [DataControl オブジェクト (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory オブジェクト (RDSServer)](../../reference/rds-api/datafactory-object-rdsserver.md)   
 [領域スペースオブジェクト (RDS)](../../reference/rds-api/dataspace-object-rds.md)   
 [RDS のシナリオ](./rds-scenario.md)   
 [RDS チュートリアル](./rds-tutorial.md)   
 [RDS の使用方法とセキュリティ](./rds-usage-and-security.md)