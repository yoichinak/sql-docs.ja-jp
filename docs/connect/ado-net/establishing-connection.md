---
title: 接続の確立
description: SqlClient プロバイダーで SQL Server に接続するた場合のガイドライン。
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 3af512f3-87d9-4005-9e2f-abb1060ff43f
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 2eb3c7d996463b9c581ea60bc11f853a5d131582
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419748"
---
# <a name="establishing-connection"></a>接続の確立

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SQL Server に接続するには、Microsoft SqlClient Data Provider for SQL Server の <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトを使用します。 安全な接続文字列の格納および取得については、「[接続情報の保護](protecting-connection-information.md)」を参照してください。

## <a name="closing-connections"></a>接続の終了

接続がプールに返されるようにするために、接続を使い終えたら必ず接続を終了することをお勧めします。 Visual Basic または C# の `Using` ブロックは、コードがこのブロックを終了したときに接続を破棄します。これは、未処理の例外の場合でも実行されます。 詳しくは、「[using ステートメント](/dotnet/docs/csharp/language-reference/keywords/using-statement.md)」および「[Using ステートメント](/dotnet/docs/visual-basic/language-reference/statements/using-statement.md)」をご覧ください。

接続オブジェクトの `Close` または `Dispose` メソッドを使用することもできます。 明示的に終了されていない接続は、プールに追加したり返したりすることができないことがあります。 たとえば、スコープ外に出ても、明示的に終了されていない接続は、最大プール サイズに達した時点でその接続がまだ有効である場合にだけ接続プールに返されます。

> [!NOTE]
> クラスの `Finalize` メソッド内で、**Connection**、**DataReader**、またはその他のマネージド オブジェクトの `Close` または `Dispose` を呼び出さないでください。 終了処理では、クラスに直接所有されているアンマネージ リソースだけを解放してください。 クラスがアンマネージ リソースを所有していない場合は、クラス定義に `Finalize` メソッドを含めないでください。 詳しくは、「[ガベージ コレクション](/dotnet/docs/standard/garbage-collection/index.md)」をご覧ください。

> [!NOTE]
> 接続が接続プールからフェッチされたり接続プールに返されたりしたとき、ログイン イベントとログアウト イベントはサーバーで発生しません。これは、接続プールに返されても接続は実際には終了していないためです。 詳しくは、「[SQL Server の接続プール (ADO.NET)](sql-server-connection-pooling.md)」をご覧ください。

## <a name="connecting-to-sql-server"></a>SQL Server への接続

有効な文字列フォーマットの名前および値については、<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlConnection> プロパティを参照してください。 また、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> クラスを使用すると、構文的に正しい接続文字列を実行時に作成できます。 詳細については、「[接続文字列ビルダー](connection-string-builders.md)」をご覧ください。

SQL Server のデータベースへの接続を開いて確立する方法を次のサンプル コードに示します。

[!code-csharp[SqlConnection.Open#1](~/../sqlclient/doc/samples/SqlConnection_Open.cs#1)]

### <a name="integrated-security-and-aspnet"></a>統合セキュリティと ASP.NET

SQL Server 統合セキュリティ (セキュリティ接続とも呼ばれます) を使用すると、SQL Server に接続するときに保護が提供されます。これは、接続文字列でユーザー ID とパスワードが公開されず、接続を認証するための推奨される方法であるためです。 統合セキュリティでは、実行中のプロセスの現在のセキュリティ ID またはトークンを使用します。 デスクトップ アプリケーションの場合、この ID は、通常、現在ログオンしているユーザーの ID です。

ASP.NET アプリケーションのセキュリティ ID は、他のオプションのうちのいずれかに設定することもできます。 SQL Server に接続するときに ASP.NET アプリケーションが使用するセキュリティ ID の詳細については、「[ASP.NET の偽装](/previous-versions/aspnet/xh507fc5(v=vs.100))」、「[ASP.NET の認証](/previous-versions/aspnet/eeyk640h(v=vs.100))」、および「[方法: Windows 統合セキュリティを使用して SQL Server にアクセスする](/previous-versions/aspnet/bsz5788z(v=vs.100))」を参照してください。

## <a name="see-also"></a>関連項目

- [データ ソースへの接続](connecting-to-data-source.md)
- [接続文字列](connection-strings.md)
