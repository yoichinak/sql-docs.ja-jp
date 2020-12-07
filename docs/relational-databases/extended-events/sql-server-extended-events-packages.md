---
title: SQL Server 拡張イベント パッケージ
description: パッケージは、SQL Server 拡張イベント オブジェクトのコンテナーです。 この記事では、パッケージに含めることができるオブジェクトについて説明します。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], packages
- xe
ms.assetid: 6bcb04fc-ca04-48f4-b96a-20b604973447
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7cf573478ce602b15718a54cfb71b03b243d601b
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867051"
---
# <a name="sql-server-extended-events-packages"></a>SQL Server 拡張イベント パッケージ

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  パッケージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベント オブジェクトのコンテナーです。 拡張イベント パッケージには、次の 3 種類があります。  
  
-   package0 : 拡張イベント システム オブジェクト。 既定のパッケージです。  
  
-   sqlserver : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関連オブジェクト。  
  
-   sqlos : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オペレーティング システム (SQLOS) 関連オブジェクト。  
  
> [!NOTE]  
>  SecAudit パッケージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査で使用されます。 パッケージ内のオブジェクトは、拡張イベントのデータ定義言語 (DDL) を通じて提供されることはありません。  
  
 パッケージは、名前、GUID、および、パッケージを含んでいるバイナリ モジュールで識別されます。 詳細については、「[sys.dm_xe_packages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql.md)」を参照してください。  
  
 パッケージには、次のいずれかまたはすべてのオブジェクトを含めることができます。この点については、このトピックの後半で詳しく説明します。  
  
-   events  
  
-   対象サーバー  
  
-   Actions  
  
-   型  
  
-   述語  
  
-   マップ  
  
 1 つのイベント セッションに異なるパッケージのオブジェクトを混在させることもできます。 詳細については、「 [SQL Server 拡張イベント セッション](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)」を参照してください。  
  
## <a name="package-contents"></a>パッケージの内容  
 次の図は、パッケージ内に存在することのできるオブジェクトを示しています。これらは、モジュール内に格納されます。 モジュールは、実行可能ファイルかダイナミック リンク ライブラリ (DLL) です。  
  
 ![モジュール、パッケージ、およびオブジェクトの関係](../../relational-databases/extended-events/media/xepackagesobjects.gif "モジュール、パッケージ、およびオブジェクトの関係")  
  
### <a name="events"></a>events  
 イベントは、プログラム ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]など) の実行パスにおける、監視対象となる地点です。 イベントは、監視対象の地点まで到達したという事実のほか、イベントが生成された時点の状態情報を伴って発生します。  
  
 イベントは、トレースを行う目的、またはアクションのトリガーを起動する目的でのみ使用できます。 これらのアクションは同期的に実行される場合と非同期的に実行される場合とがあります。  
  
> [!NOTE]  
>  イベントは、その発生に呼応して起動されるアクションについての情報は一切持ちません。  
  
 パッケージが拡張イベントに登録された後で、パッケージ内の一連のイベントを変更することはできません。  
  
 すべてのイベントは、その内容を定義するバージョン管理されたスキーマを持ちます。 このスキーマは、適切に定義された型を持つイベント列で構成されます。 特定の型のイベントは、常にそのデータを、スキーマで指定された順序とまったく同じ順序で提供する必要があります。 ただし、イベント ターゲットは、必ずしも提供されたすべてのデータを利用する必要はありません。  
  
#### <a name="event-categorization"></a>イベントの分類  
 拡張イベントには、Event Tracing for Windows (ETW) に似たイベント分類モデルが使用されます。 分類には、チャネルとキーワードという 2 つのイベント プロパティが使用されます。 これらのプロパティを使用することにより、拡張イベントを ETW やそのツールと連携させることができます。  
  
 **Channel**  
  
 チャネルは、イベントの対象ユーザーを識別します。 次の表でこれらのチャネルについて説明します。  
  
|期間|定義|  
|----------|----------------|  
|[Admin]|管理イベントの対象は、主にエンド ユーザー、管理者、およびサポートです。 管理チャネルのイベントは、管理者が対応できる明確な解決策が存在する問題を示します。 たとえば、アプリケーションがプリンターに接続できなかった場合に発生するイベントなどがあります。 これらのイベントには、詳しい解説が付属するか、問題の解決方法をユーザーに伝えるメッセージが関連付けられています。|  
|運用時|運用イベントは、問題や事象の分析および診断のために使用されます。 問題や事象に応じたツールまたはタスクを起動する目的で使用できます。 たとえば、プリンターがシステムに追加されたり、システムから削除された場合に発生するイベントなどがあります。|  
|分析|非常に多くの分析イベントが公開されています。 プログラムの動作を説明するもので、主にパフォーマンス調査に用いられます。|  
|デバッグ|デバッグ イベントは、開発者がデバッグ時に問題を診断する目的でのみ使用されます。<br /><br /> デバッグ チャネルのイベントでは、実装固有の内部状態データが返されます。 スキーマ、およびこのイベントによって返されるデータは、SQL Server の将来のバージョンで変更または無効化される可能性があります。 そのため、デバッグ チャネルのイベントは、SQL Server の将来のバージョンで予告なしに変更または削除されることがあります。|  
  
 **Keyword**  
  
 キーワードはアプリケーション固有の情報です。キーワードを使用すると、関連するイベントをより詳細に分類でき、セッションで使用するイベントの指定や取得を簡単に行うことができます。 次のクエリを使用すると、キーワード情報を取得できます。  
  
```  
select map_value Keyword from sys.dm_xe_map_values  
where name = 'keyword_map'  
```  
  
> [!NOTE]  
>  キーワードを使用すると、現在の SQL トレース イベントのグループを緊密に対応付けることができます。  
  
### <a name="targets"></a>対象サーバー  
 ターゲットは、イベントのコンシューマーです。 ターゲットは、イベントを開始したスレッド上で同期的に、またはシステムによって提供されたスレッド上で非同期的に、イベントを処理します。 拡張イベントには、複数のターゲットが用意されており、イベント出力を転送する目的で必要に応じて使用できます。 詳細については、「 [SQL Server 拡張イベント ターゲット](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))」を参照してください。  
  
### <a name="actions"></a>Actions  
 アクションは、プログラムがイベントに呼応して実行する特定の (または一連の) 応答です。 アクションはイベントに関連付けられます。各イベントには、それぞれ異なる一連のアクションが関連付けられる場合もあります。  
  
> [!NOTE]  
>  特定のイベント セット用のアクションを、未知のイベントに関連付けることはできません。  
  
 イベントに関連付けられたアクションは、そのイベントが発生したスレッドで同期的に呼び出されます。 アクションの種類と機能は多岐にわたります。 アクションを使ってできることの例を次に示します。  
  
-   スタック ダンプをキャプチャしてデータを検査する。  
  
-   変更可能なストレージを使って状態情報をローカル コンテキストに保存する。  
  
-   イベント データを集計する。  
  
-   イベント データにデータを追加する。  
  
 アクションの代表的な使用例を次に示します。  
  
-   スタック ダンプ機能  
  
-   実行プランの検出 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のみ)  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] スタック コレクション ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のみ)  
  
-   実行時の統計計算  
  
-   例外時のユーザー入力の収集  
  
### <a name="predicates"></a>述語  
 述語は、処理するイベントを評価するために使用される一連の論理規則です。 拡張イベントのユーザーは、特定の条件に基づいてイベント データを選択的にキャプチャできます。  
  
 述語ではデータをローカル コンテキストに保存できます。そのデータを使って、 *n* 分ごと、またはイベントが *n* 回発生するたびに true を返す述語を作成できます。 さらに、このローカル コンテキストの格納域を使用して述語を動的に更新することにより、イベントに同様のデータが格納されていた場合に、それ以上のイベントの発生を抑制することもできます。  
  
 述語には、イベント固有のデータに加え、スレッド ID などのコンテキスト情報を取得する機能があります。 述語は完全なブール式として評価され、式全体が false であると判明した時点ですぐに結果を返すことができます。  
  
> [!NOTE]  
>  二次的に作用する述語は、先行する述語が false と判定された場合、評価されない可能性があります。  
  
### <a name="types"></a>型  
 データは一連のバイトの集合であるため、そのバイト集合の長さと特性がわからなければ、データを解釈することはできません。 この情報は、Type オブジェクトにカプセル化されています。 パッケージ オブジェクトには、次の型が用意されています。  
  
-   イベント  
  
-   action  
  
-   ターゲット (target)  
  
-   pred_source  
  
-   pred_compare  
  
-   type  
  
 詳細については、「[sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)」を参照してください。  
  
### <a name="maps"></a>マップ  
 内部値はマップ テーブルによって文字列に対応付けられます。これにより、ユーザーは、その値が何を表しているのかを知ることができます。 内部値について単に数値を取得できるだけでなく、意味のある説明を取得できます。 次のクエリは、マップ値の取得方法を示しています。  
  
```  
select map_key, map_value from sys.dm_xe_map_values  
where name = 'lock_mode'  
```  
  
 以下は前述のクエリの出力結果です。  
  
 `map_key     map_value`  
  
 `---------------------`  
  
 `0           NL`  
  
 `1           SCH_S`  
  
 `2           SCH_M`  
  
 `3           S`  
  
 `4           U`  
  
 `5           X`  
  
 `6           IS`  
  
 `7           IU`  
  
 `8           IX`  
  
 `9           SIU`  
  
 `10          SIX`  
  
 `11          UIX`  
  
 `12          BU`  
  
 `13          RS_S`  
  
 `14          RS_U`  
  
 `15          RI_NL`  
  
 `16          RI_S`  
  
 `17          RI_U`  
  
 `18          RI_X`  
  
 `19          RX_S`  
  
 `20          RX_U`  
  
 `21          RX_X`  
  
 `21          RX_X`  
  
 たとえば、このテーブルに mode という名前の列があり、その値が 5 であると仮定します。 このテーブルによると、5 は X に対応しており、そこからロックの種類が Exclusive であることがわかります。  
  
## <a name="see-also"></a>参照  
 [SQL Server 拡張イベント セッション](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)   
 [SQL Server 拡張イベント エンジン](../../relational-databases/extended-events/sql-server-extended-events-engine.md)   
 [SQL Server 拡張イベント ターゲット](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))  
  
