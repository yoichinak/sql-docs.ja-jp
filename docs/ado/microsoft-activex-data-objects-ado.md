---
description: Microsoft ActiveX Data Objects (ADO)
title: Microsoft ActiveX データオブジェクト (ADO) |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
author: rothja
ms.author: jroth
ms.openlocfilehash: a63b254397e45fdba56f3d86cdcf45069f9265fb
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721243"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ActiveX データオブジェクトは、特定のバックエンドエンジンに依存しないことを意味するプログラミングモデルです。 ただし、現在のところ、ADO モデルをサポートするエンジンは OLE DB のみです。 OLE db Provider for ODBC には、多くのネイティブ OLE DB プロバイダーが用意されています。 ADO は、C++ および Visual Basic プログラムで SQL Server およびその他のデータベースに接続するために使用されます。 もちろん、クラウド内の Azure SQL Database に接続することもできます。

この記事の各セクションでは、ADO のコンポーネントについて説明します。

> [!NOTE]
> ADO.NET は ADO とは異なります。 ADO.NET、およびその他の多くの SQL 接続ドライバーとその言語については [SQL Server ドライバー](../connect/sql-connection-libraries.md)をご覧ください。

  
## <a name="ado"></a>ADO (ADO)  
 Microsoft ActiveX データオブジェクト (ADO) を使用すると、クライアントアプリケーションは、OLE DB プロバイダーを介してさまざまなソースからのデータにアクセスして操作できます。 主な利点は、使いやすさ、高速、メモリオーバーヘッド、およびディスクフットプリントが小さいことです。 ADO は、クライアント/サーバーおよび Web ベースのアプリケーションを構築するための主要な機能をサポートしています。  
  
## <a name="ado-md"></a>ADO MD (ADO MD)  
 Microsoft ActiveX データオブジェクト (多次元) (ADO MD) を使用すると、Microsoft Visual Basic、Microsoft Visual C++ などの言語からの多次元データに簡単にアクセスできます。 ADO MD により、Microsoft ActiveX データオブジェクト (ADO) が拡張され、CubeDef オブジェクトや Cellset オブジェクトなどの多次元データに固有のオブジェクトが追加されます。 ADO MD を使用すると、多次元スキーマの参照、キューブのクエリ、および結果の取得を行うことができます。  
  
 ADO と同様に、ADO MD は、基になる OLE DB プロバイダーを使用してデータにアクセスします。 ADO MD を使用するには、プロバイダーが OLAP 仕様の OLE DB で定義されている多次元データプロバイダー (.MDP) である必要があります。 MDPs は、表形式のビューにデータを表示する表形式のデータプロバイダー (TDPs) ではなく、多次元ビューにデータを表示します。 プロバイダーでサポートされている特定の構文と動作の詳細については、OLAP OLE DB プロバイダーのドキュメントを参照してください。  
  
## <a name="rds"></a>RDS  
 リモートデータサービス (RDS) は ADO の機能の1つです。この機能を使用すると、サーバーからクライアントアプリケーションまたは Web ページにデータを移動し、クライアント上のデータを操作して、1回のラウンドトリップでサーバーに更新を返すことができます。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、  [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="adox"></a>ADOX  
 データ定義言語およびセキュリティ用の Microsoft ActiveX データオブジェクト拡張機能 (ADOX) は、ADO オブジェクトとプログラミングモデルの拡張機能です。 ADOX には、スキーマの作成と変更、およびセキュリティのためのオブジェクトが含まれています。 スキーマ操作に対するオブジェクトベースのアプローチであるため、ネイティブ構文の違いに関係なく、さまざまなデータソースに対して機能するコードを記述できます。  
  
 ADOX は、中核となる ADO オブジェクトに関連するライブラリです。 テーブルやプロシージャなどのスキーマオブジェクトを作成、変更、および削除するための追加のオブジェクトを公開します。 また、ユーザーとグループを管理したり、オブジェクトに対する権限を許可および取り消すためのセキュリティオブジェクトも含まれます。  
  
## <a name="documentation"></a>ドキュメント  
 [ADO セキュリティ デザイン機能に関する問題](./guide/ado-security-design-issues.md)  
  
 [ADO プログラマー ガイド](./guide/ado-programmer-s-guide.md)  
  
 ADO、RDS、ADO MD、および ADOX の使用方法について説明します。  
  
 [ADO プログラマー リファレンス](./reference/ado-programmer-s-reference.md)  
  
 ADO ドキュメントのこのセクションには、各 ADO、RDS、ADO MD、ADOX オブジェクト、コレクション、プロパティ、動的プロパティ、メソッド、イベント、および列挙に関するトピックが含まれています。  
  
 [ADO の用語集](./ado-glossary.md)  
  
## <a name="support"></a>サポート  
 ADO の問題に関する無料ヘルプを表示するには、ADO パブリックニュースグループに投稿してください。 このニュースグループは、ADO をカバーする Microsoft 製品サポートサービス (PSS) サポート担当者と、その他の経験豊富な ADO 開発者によって監視されています。  
  
 サポートオプションの詳細については、Microsoft ヘルプとサポートの Web サイトを参照してください。