---
title: 非同期操作
description: .NET Framework で使用されている非同期モデルに基づいて設計された API を使用して、非同期データベース操作を実行する方法について説明します。
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 3923db97ce144662f7fe5410c13278862d1ab6a1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725681"
---
# <a name="asynchronous-operations"></a>非同期操作

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

コマンドの実行など、データベースでの一部の操作は、完了までに長時間かかることがあります。 このような場合、シングルスレッド アプリケーションでは、他の操作をブロックしなければならず、そのコマンドの完了を待ってから独自の操作を続行する必要があります。 これに対して、長時間にわたる操作をバックグラウンド スレッドに割り当てることができれば、フォアグラウンド スレッドがアクティブなまま操作を続行できます。 たとえば、Windows アプリケーションでは、操作を実行中のユーザー インターフェイス スレッドの応答性を維持しながら、時間のかかる操作をバックグラウンド スレッドに委任することができます。  
  
.NET には、開発者がバックグラウンド スレッドを利用し、ユーザー インターフェイスや優先順位の高いスレッドを解放してその <xref:Microsoft.Data.SqlClient.SqlCommand> クラスの他の操作を完了するために使用できる、標準の非同期デザイン パターンがいくつか用意されています。 特に、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A>、および <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> メソッドと、<xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A>、および <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> メソッドとのペアによって、非同期動作がサポートされています。  
  
> [!NOTE]
>  非同期プログラミングは .NET のコアとなる機能です。 開発者が使用できるさまざまな非同期技法の詳細については、「[同期メソッドの非同期呼び出し](/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)」を参照してください。  
  
ADO.NET 機能で非同期技法を使用しても特別な考慮事項は追加されませんが、マルチスレッド アプリケーションを作成する利点と落とし穴に注意することが重要です。 このセクションに示す例は、マルチスレッド機能を組み込むアプリケーションを構築する際に考慮すべき重要な問題を提示しています。  
  
## <a name="in-this-section"></a>このセクションの内容  
[コールバックを使用する Windows アプリケーション](windows-applications-callbacks.md)  
この例では、非同期コマンドを安全に実行し、異なるスレッドのフォームと内容との対話を正しく処理する方法を示します。  
  
[待機ハンドルを使用する ASP.NET アプリケーション](aspnet-apps-use-wait-handles.md)  
この例では、ASP.NET ページから複数の同時実行コマンドを実行し、すべてのコマンドの終了時に Wait ハンドルを使用して操作を管理する方法を示します。  
  
[コンソール アプリケーションでのポーリング](poll-console-applications.md)  
この例では、ポーリングを使用して非同期コマンドの実行をコンソール アプリケーションで待機する方法を示します。 この技法は、クラス ライブラリまたはユーザー インターフェイスを持たないその他のアプリケーションでも有効です。  
  
## <a name="next-steps"></a>次のステップ
- [SQL Server と ADO.NET](index.md)
- [同期メソッドの非同期呼び出し](/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)