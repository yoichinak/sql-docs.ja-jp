---
description: システム ベース テーブル
title: システムベーステーブル |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system base tables [SQL Server]
- hobt [SQL Server]
- base tables
ms.assetid: 31f2df90-651f-4699-8067-19f59b60904f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 09f898ac65e48977b98b55c1f6b5e5ed9057ee49
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810212"
---
# <a name="system-base-tables"></a>システム ベース テーブル
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  システム ベース テーブルは、特定のデータベースのメタデータを実際に格納する、基になるテーブルです。 **Master**データベースには、他のどのデータベースにも存在しない追加のテーブルが含まれているので、この点で特別なことです。 これらのテーブルには、サーバー全体のスコープを持つ永続化されたメタデータが含まれています。  
  
> [!IMPORTANT]  
>  システム ベース テーブルは、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]内のみで使用されるテーブルであり、一般ユーザーが使用するテーブルではありません。 これらは変更される可能性があり、互換性は保証されていません。  
  
## <a name="system-base-table-metadata"></a>システム ベース テーブルのメタデータ  
 データベースに対する CONTROL、ALTER、または VIEW DEFINITION 権限を持つ権限付与対象ユーザーは、システムベーステーブルのメタデータを使用して、システム **のカタログビュー** を表示できます。 権限付与対象ユーザーは、 [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md) や [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)などの組み込み関数を使用して、システムベーステーブルの名前とオブジェクト id を解決することもできます。  
  
 システムベーステーブルにバインドするには、ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 専用管理者接続 (DAC) を使用してのインスタンスに接続する必要があります。 DAC で接続せずにシステム ベース テーブルから SELECT クエリを実行しようとすると、エラーが発生します。  
  
> [!IMPORTANT]  
>  DAC を使用したシステムベーステーブルへのアクセスは、担当者向けに設計されて [!INCLUDE[msCoName](../../includes/msconame-md.md)] おり、サポートされている顧客シナリオではありません。  
  
## <a name="system-base-tables"></a>システム ベース テーブル  
 次の表に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム ベース テーブルの一覧とその説明を示します。  
  
|ベーステーブル|説明|  
|----------------|-----------------|  
|**sys.sysschobjs**|すべてのデータベースに存在します。 各行は、データベース内のオブジェクトを表します。|  
|**sys.sysbinobjs**|すべてのデータベースに存在します。 データベース内の Service Broker エンティティごとに1行のデータを格納します。 Service Broker エンティティには次のものがあります。<br /><br /> メッセージの種類<br /><br /> サービスコントラクト<br /><br /> サービス<br /><br /> 名前および型では、固定されているバイナリ照合順序を使用します。|  
|**sys.sysclsobjs**|すべてのデータベースに存在します。 次のような共通プロパティを共有する、分類されたエンティティごとに1行の情報を格納します。<br /><br /> アセンブリ<br /><br /> バックアップ デバイス<br /><br /> フルテキスト カタログ<br /><br /> パーティション関数<br /><br /> パーティション構成<br /><br /> ファイル グループ<br /><br /> 隠ぺいキー|  
|**sys.sysnsobjs**|すべてのデータベースに存在します。 名前空間スコープのエンティティごとに1行の値を格納します。 このテーブルは、XML コレクション エンティティの格納に使用されます。|  
|**sys.syscolpars**|すべてのデータベースに存在します。 テーブル、ビュー、またはテーブル値関数内のすべての列に対応する行が含まれています。 また、プロシージャまたは関数のパラメーターごとの行も格納します。|  
|**sys.systypedsubobjs**|すべてのデータベースに存在します。 型指定されたサブエンティティごとに 1 行のデータを格納します。 パーティション関数のパラメーターだけがこのカテゴリに分類されます。|  
|**sys.sysidxstats**|すべてのデータベースに存在します。 テーブルおよびインデックス付きビューのインデックスまたは統計ごとに 1 行のデータを格納します。<br /><br /> 注: すべてのインデックス (ヒープを除く) は、インデックスと同じ名前の統計に関連付けられています。|  
|**sys.sysiscols**|すべてのデータベースに存在します。 保持されるインデックスと統計の列ごとに1行のデータを格納します。|  
|**sys.sysscalartypes**|すべてのデータベースに存在します。 ユーザー定義型またはシステム型ごとに1行の値を格納します。|  
|**sys.sysdbreg**|**Master**データベースのみに存在します。 登録されたデータベースごとに 1 行のデータを格納します。|  
|**sys.sysxsrvs**|**Master**データベースのみに存在します。 ローカル サーバー、リンク サーバー、またはリモート サーバーごとに 1 行のデータを格納します。|  
|**sys.sysrmtlgns**|このシステムベーステーブルは、 **master** データベースにのみ存在します。 リモートログインマッピングごとに1行の値を格納します。 対応するサーバーから送信されてきたと称する受信ログインを、実際のローカル ログインにマップするために使用します。|  
|**sys.syslnklgns**|**Master**データベースのみに存在します。 リンク ログイン マッピングごとに 1 行のデータを格納します。 リンクされたログインのマッピングは、リモートプロシージャコールおよびローカルサーバーから対応するリンクサーバーに送信される分散クエリによって使用されます。|  
|**sys.sysxlgns**|**Master**データベースのみに存在します。 サーバープリンシパルごとに1行の値を格納します。|  
|**sys.sysdbfiles**|すべてのデータベースに存在します。 列 **dbid** が0の場合、行はこのデータベースに属するファイルを表します。 **Master**データベースでは、列**dbid**を0以外にすることができます。 その場合、該当する行は master ファイルを表します。|  
|**sys.sysusermsg**|**Master**データベースのみに存在します。 各行は、ユーザー定義のエラーメッセージを表します。|  
|**sys.sysprivs**|すべてのデータベースに存在します。 データベース レベルまたはサーバー レベルの権限ごとに 1 行のデータを格納します。<br /><br /> 注: サーバーレベルの権限は **master** データベースに格納されます。|  
|**sys.sysowners**|すべてのデータベースに存在します。 各行は、データベースプリンシパルを表します。|  
|**sys.sysobjkeycrypts**|すべてのデータベースに存在します。 オブジェクトに関連付けられた対称キー、暗号化、または暗号化プロパティごとに1行の値を格納します。|  
|**sys.syscerts**|すべてのデータベースに存在します。 データベース内の証明書ごとに 1 行のデータを格納します。|  
|**sys.sysasymkeys**|すべてのデータベースに存在します。 各行は、非対称キーを表します。|  
|**ftinds**|すべてのデータベースに存在します。 データベース内のフルテキスト インデックスごとに 1 行のデータを格納します。|  
|**sys.sysxprops**|すべてのデータベースに存在します。 拡張プロパティごとに 1 行のデータを格納します。|  
|**sys.sysallocunits**|すべてのデータベースに存在します。 ストレージアロケーションユニットごとに1行のデータを格納します。|  
|**sys.sysrowsets**|すべてのデータベースに存在します。 インデックスまたはヒープのパーティション行セットごとに1行の値を格納します。|  
|**sys.sysrowsetrefs**|すべてのデータベースに存在します。 行セット参照へのインデックスごとに1行の値を格納します。|  
|**sys.syslogshippers 業者**|**Master**データベースのみに存在します。 データベース ミラーリング監視サーバーごとに 1 行のデータを格納します。|  
|**sys.sysremsvcbinds**|すべてのデータベースに存在します。 リモートサービスバインドごとに1行の値を格納します。|  
|**sys.sysconvgroup**|すべてのデータベースに存在します。 Service Broker 内のサービスインスタンスごとに1行の値を格納します。|  
|**sys.sysxmitqueue**|すべてのデータベースに存在します。 Service Broker 転送キューごとに1行の値を格納します。|  
|**sys.sysdesend**|すべてのデータベースに存在します。 Service Broker メッセージ交換の送信エンドポイントごとに 1 行のデータを格納します。|  
|**sys.sysdercv**|すべてのデータベースに存在します。 Service Broker メッセージ交換の受信エンドポイントごとに1行の値を格納します。|  
|**sys.sysendpts**|**Master**データベースのみに存在します。 サーバー内で作成されたエンドポイントごとに 1 行のデータを格納します。|  
|**sys.syswebmethods**|**Master**データベースのみに存在します。 サーバーで作成される SOAP 対応 HTTP エンドポイントで定義されている SOAP メソッドごとに1行の値を格納します。|  
|**sys.sysqnames**|すべてのデータベースに存在します。 4バイト ID トークンの名前空間または修飾名ごとに1行のデータを格納します。|  
|**sys.sysxmlcomponent**|すべてのデータベースに存在します。 各行は、XML スキーマ コンポーネントを表します。|  
|**sys.sysxmlfacet**|すべてのデータベースに存在します。 XML 型定義の XML ファセット (制限) ごとに1行の値を格納します。|  
|**sys.sysxmlplacement**|すべてのデータベースに存在します。 XML コンポーネントの XML 配置ごとに 1 行のデータを格納します。|  
|**sys.syssingleobjrefs**|すべてのデータベースに存在します。 一般的な N 対 1 参照ごとに 1 行のデータを格納します。|  
|**sys.sysmultiobjrefs**|すべてのデータベースに存在します。 一般的な N から N への参照ごとに1行の値を格納します。|  
|** Objvalues のsys.sys**|すべてのデータベースに存在します。 エンティティの一般値プロパティごとに1行の値を格納します。|  
|**sys.sysguidrefs**|すべてのデータベースに存在します。 GUID で分類された ID 参照ごとに 1 行のデータを格納します。|  
  
## <a name="updating-system-base-tables"></a>システムベーステーブルの更新    
システムテーブル内のデータは、システムカタログビューを使用して表示できます。 システムベーステーブルのメタデータを更新するには、適切な TSQL インターフェイス (DDL ステートメントなど) を使用します。 システムテーブルを手動で更新することはできません。 SQL Server は、システムテーブルに対して直接更新を実行するときに、次のメッセージを報告します。

### <a name="a-system-table-is-manually-updated"></a>システムテーブルは手動で更新されます
メッセージ 17659: 警告: システム テーブル <id> がデータベース <id> で直接更新されました。キャッシュの一貫性が維持されていない可能性があります。 SQL Server を再起動してください。

### <a name="starting-a-database-with-a-system-table-that-was-manually-updated"></a>手動で更新されたシステム テーブルを使用してデータベースを開始する
メッセージ 3859: 警告: システムカタログがデータベース ID 17 で直接更新されました。これは date_time で最近行われたものです。

### <a name="executing-the-dbcc_checkdb-command-after-a-system-table-is-manually-updated"></a>システムテーブルを手動で更新した後に DBCC_CHECKDB コマンドを実行する
メッセージ 3859: 警告: システムカタログがデータベース ID 17 で直接更新されました。これは date_time で最近行われたものです。

システムテーブルに対して手動更新を実行し、問題が発生した場合は、バックアップから復元するか、影響を受けるデータベースから新しいデータベースにデータをコピーするかを確認するメッセージが表示されることがあります。 [ユーザーアクションのエラーメッセージ](../errors-events/mssqlserver-8992-database-engine-error.md?view=sql-server-ver15#user-action)の詳細を表示します。