---
title: SqlClient のパフォーマンス カウンター
description: Windows パフォーマンス モニターまたはプログラムを使用してアプリケーションの状態とその接続リソースを監視するには、Microsoft SqlClient Data Provider for SQL Server のパフォーマンス カウンターを使用します。
ms.date: 12/04/2020
dev_langs:
- csharp
ms.assetid: 0b121b71-78f8-4ae2-9aa1-0b2e15778e57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e9d8c2edb88a9ed50b47c761d3af8aec8016065a
ms.sourcegitcommit: 5b2c47ce88f7e56552fd415c32b319009d043b56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97804295"
---
# <a name="performance-counters-in-sqlclient"></a>SqlClient のパフォーマンス カウンター

[!INCLUDE[appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient> のパフォーマンス カウンターを使用して、アプリケーションの状態と使用されている接続リソースを監視できます。 パフォーマンス カウンターは、Windows パフォーマンス モニターを使って監視できるほか、<xref:System.Diagnostics.PerformanceCounter> 名前空間の <xref:System.Diagnostics> クラスを使用することでプログラムから監視することもできます。

## <a name="available-performance-counters"></a>利用できるパフォーマンス カウンター

次の表に示すように、現在 <xref:Microsoft.Data.SqlClient> で使用できるパフォーマンス カウンターは 14 個あります。

|パフォーマンス カウンター|説明|  
|-------------------------|-----------------|  
|`HardConnectsPerSecond`|データベース サーバーに対する 1 秒あたりの接続数。|  
|`HardDisconnectsPerSecond`|データベース サーバーに対する 1 秒あたりの切断数。|  
|`NumberOfActiveConnectionPoolGroups`|アクティブな一意の接続プール グループの数。 このカウンターは、AppDomain に見つかった一意の接続文字列数によって制御されます。|  
|`NumberOfActiveConnectionPools`|接続プールの合計数。|  
|`NumberOfActiveConnections`|現在使用中のアクティブな接続の数。 **注:** このパフォーマンス カウンターは、既定では無効にされています。 このパフォーマンス カウンターを有効にするには、「[既定でオフになっているカウンターのアクティブ化](#ActivatingOffByDefault)」を参照してください。|  
|`NumberOfFreeConnections`|接続プール内の利用可能な接続数。 **注:** このパフォーマンス カウンターは、既定では無効にされています。 このパフォーマンス カウンターを有効にするには、「[既定でオフになっているカウンターのアクティブ化](#ActivatingOffByDefault)」を参照してください。|  
|`NumberOfInactiveConnectionPoolGroups`|排除対象としてマークされた一意の接続プール グループの数。 このカウンターは、AppDomain に見つかった一意の接続文字列数によって制御されます。|  
|`NumberOfInactiveConnectionPools`|最近のアクティビティが存在せず、破棄待ち状態となっている、アクティブでない接続プールの数。|  
|`NumberOfNonPooledConnections`|プールされていないアクティブな接続の数。|  
|`NumberOfPooledConnections`|接続プール インフラストラクチャによって管理されているアクティブな接続の数。|  
|`NumberOfReclaimedConnections`|アプリケーションによって `Close` も `Dispose` も呼び出されなかった場合に、ガベージ コレクションによって回収された接続の数。 **注** 明示的に終了または破棄しないと、パフォーマンスに悪影響を及ぼします。|  
|`NumberOfStasisConnections`|現在アクションの完了を待っている (そのためにアプリケーションからは使用できない) 接続の数。|  
|`SoftConnectsPerSecond`|接続プールからプルされているアクティブな接続の数。 **注:** このパフォーマンス カウンターは、既定では無効にされています。 このパフォーマンス カウンターを有効にするには、「[既定でオフになっているカウンターのアクティブ化](#ActivatingOffByDefault)」を参照してください。|  
|`SoftDisconnectsPerSecond`|接続プールに戻されているアクティブな接続の数。 **注:** このパフォーマンス カウンターは、既定では無効にされています。 このパフォーマンス カウンターを有効にするには、「[既定でオフになっているカウンターのアクティブ化](#ActivatingOffByDefault)」を参照してください。|  

### <a name="connection-pool-groups-and-connection-pools"></a>接続プール グループと接続プール

Windows 認証 (統合セキュリティ) を使用している場合、`NumberOfActiveConnectionPoolGroups` と `NumberOfActiveConnectionPools` の両方のパフォーマンス カウンターを監視する必要があります。 なぜなら、接続プール グループは接続文字列単位でマップされるためです。 統合セキュリティを使用した場合、接続文字列にマップされた接続プールの他に、個々の Windows ID 用に別々のプールが作成されます。 たとえば、同じ AppDomain に属する Fred と Julie が、どちらも `"Data Source=MySqlServer;Integrated Security=true"` という接続文字列を使用した場合、その接続文字列に対応した接続プール グループが作成され、それに加えて、2 つのプール (Fred 用と Julie 用) が作成されます。 John と Martha がまったく同じ SQL Server ログインを持った接続文字列 `"Data Source=MySqlServer;User Id=<myUserID>;Password=<myPassword>"` を使用した場合は、 **<myUserID>** の ID に対して単一のプールが作成されます。

<a name="ActivatingOffByDefault"></a>

### <a name="activate-off-by-default-counters"></a>既定でオフになっているカウンターのアクティブ化

`NumberOfFreeConnections`、`NumberOfActiveConnections`、`SoftDisconnectsPerSecond`、`SoftConnectsPerSecond` の各パフォーマンス カウンターは、既定ではオフになっています。 有効にするには、アプリケーションの構成ファイルに次の情報を追加します。

```xml  
<system.diagnostics>  
  <switches>  
    <add name="ConnectionPoolPerformanceCounterDetail"  
         value="4"/>  
  </switches>  
</system.diagnostics>  
```  

## <a name="retrieve-performance-counter-values"></a>パフォーマンス カウンター値の取得

次のコンソール アプリケーションは、アプリケーションでパフォーマンス カウンターの値を取得する方法を示しています。 情報が返されるには、Microsoft SqlClient Data Provider for SQL Server のすべてのパフォーマンス カウンターについて、接続が開かれておりアクティブである必要があります。

> [!NOTE]
> この例では、サンプルの [**AdventureWorks** データベース](../../samples/adventureworks-install-configure.md)を使用します。 サンプル コードに示されている接続文字列は、データベースがローカル コンピューターにインストールされており、かつ使用可能であること、および接続文字列で指定されたログインと一致するログインが作成されていることを前提としています。 既定のセキュリティ設定を使用するようにサーバーが構成されている場合、そのままでは Windows 認証しか許可されないため、SQL Server ログインを有効にする必要があります。 接続文字列は環境に合わせて変更してください。

### <a name="example"></a>例

[!code-csharp[SqlClient_PerformanceCounter#1](~/../sqlclient/doc/samples/SqlClient_PerformanceCounter.cs#1)]

## <a name="see-also"></a>関連項目

- [データ ソースへの接続](connecting-to-data-source.md)
- [ランタイム プロファイリング](/dotnet/framework/debug-trace-profile/runtime-profiling)
- [パフォーマンスしきい値の監視の概要](/previous-versions/visualstudio/visual-studio-2008/bd20x32d(v=vs.90))
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
