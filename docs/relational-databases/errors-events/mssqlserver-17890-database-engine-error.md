---
description: MSSQLSERVER_17890
title: MSSQLSERVER_17890
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 17890 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 09ea56c914385ee25a889262259a13073ad595d4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196607"
---
# <a name="mssqlserver_17890"></a>MSSQLSERVER_17890
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|17890|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|SRV_WS_TRIMMED|
|メッセージ テキスト|SQL Server プロセス メモリのかなりの部分がページ アウトされています。結果として、パフォーマンスが低下する可能性があります。 継続時間: %d 秒。 ワーキング セット (KB): %I64d、コミット メモリ (KB): %I64d、メモリ使用率: %d%%。|
||

## <a name="explanation"></a>説明

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログまたは Windows アプリケーション イベント ログに、次のエラー メッセージが表示される場合があります。

> SQL Server プロセス メモリのかなりの部分がページ アウトされています。結果として、パフォーマンスが低下する可能性があります。 期間:0 秒。 作業セット (KB):3383250、コミット済み (KB):9112480、メモリ使用率:37%。

また、クエリの実行および SQL Server に対するその他のすべての操作によって、パフォーマンスが急激に低下することがあります。

## <a name="cause"></a>原因

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスに関するさまざまなメモリ関連情報を監視します。 このケースでは、プロセスのワーキング セットが、コミット済みプロセス メモリの 50% 未満であることが検出されました。 その結果、この警告が出力されます。 この警告の通常の原因は次のとおりです。

- オペレーティング システムによって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコミット済みメモリの大部分がページング ファイルにページ アウトされています。
- これは、他のアプリケーションやオペレーティング システムのニーズからのメモリの需要が急激に増加していることが原因である可能性があります。
- また、これは特定のデバイス ドライバーのニーズによって、連続するメモリ割り当てが要求されるときに発生することもあります。

## <a name="user-action"></a>ユーザー アクション

物理メモリ内のバッファー プール用に割り当てられたメモリをロックすることで、Windows オペレーティング システムによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスのバッファー プール メモリがページ アウトされるのを防ぐことができます。 メモリをロックするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの開始アカウントとして使用されるユーザー アカウントに、Lock pages in memory ユーザー権利を割り当てます。 ただし、このソリューションを実装する前に、SQL Server のインスタンスに対して "Lock pages in memory" ユーザー権利を割り当てる前に、「[SQL Server メモリがページ アウトされる原因](#what-causes-sql-server-memory-to-be-paged-out)」と重要な考慮事項に関するセクションを見直してください。

> [!NOTE]
> Lock Pages in Memory を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって管理されるメモリがページ アウトされないようにすることができます。ただし、スレッド スタック、EXE とあらゆる DLL イメージ、ヒープ メモリ、CLR メモリは、引き続き OS によってページ アウトされます。
>
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 SP1 の累積的な更新プログラム 2 以降、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Standard Edition と Enterprise Edition の両方で、Lock pages in memory ユーザー権利を使用できます。 ロックされたページのサポートの詳細については、「[KB970070 - SQL Server Standard Edition (64 ビット) システムのロックされたページのサポート](https://support.microsoft.com/help/970070)」を参照してください。

Lock pages in memory ユーザー権利を割り当てるには、次の手順を実行します。

1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックして、「*gpedit.msc*」と入力してから、 **[OK]** をクリックします。
1. [グループ ポリシー] ダイアログ ボックスが表示されます。
1. **[コンピューターの構成]** を展開し、 **[Windows の設定]** を展開します。
1. **[セキュリティの設定]** を展開し、 **[ローカル ポリシー]** を展開します。
1. [ユーザー権利の割り当て] をクリックし、 **[Lock pages in memory]** をダブルクリックします。
1. **[ローカル セキュリティ ポリシーの設定]** ダイアログ ボックスで、 **[ユーザーの追加]** または **[グループの追加]** をクリックします。
1. **[ユーザーの選択]** または **[グループの選択]** ダイアログ ボックスで、Sqlservr.exe ファイルを実行するアクセス許可があるアカウントを追加してから、 **[OK]** をクリックします。
1. **[グループ ポリシー]** ダイアログ ボックスを閉じます。
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再開します。

Lock pages in memory ユーザー権利を割り当てて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再起動した後は、Windows オペレーティング システムで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス内のバッファー プール メモリがページ アウトされなくなります。 ただし、Windows オペレーティング システムでは、引き続き [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス内のバッファー プール以外のメモリをページ アウトできます。

そのユーザー権利が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスによって使用されていることを検証するには、起動時に次のメッセージが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに書き込まれていることを確認します。"バッファー プールにロックされたページを使用しています"

このメッセージは SQL Server にのみ適用されます。 ERRORLOG 内のこのメッセージの詳細については、「[ローカル システムで Lock pages in memory の権限を割り当てる必要がありますか](https://techcommunity.microsoft.com/t5/sql-server-support/do-i-have-to-assign-the-lock-pages-in-memory-privilege-for-local/ba-p/315426)」にアクセスしてください。

Windows オペレーティング システムによってバッファー プール以外のメモリがページ アウトされると、パフォーマンスの問題が発生する可能性があります。 ただし、「説明」セクションに記載されているエラー メッセージは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログには記録されません。

## <a name="what-causes-sql-server-memory-to-be-paged-out"></a>SQL Server メモリがページ アウトされる原因

この問題を引き起こす可能性がある問題には、大きく次の 3 つのカテゴリに分けられます。

- アプリケーションに関連した問題:すべてのアプリケーションで使用可能な物理メモリを使い果たし、OS で新しいアプリケーション要求のためのリソースとしてメモリを解放する必要があります。 通常、ここでのアプローチは、メモリを使い果たしているアプリケーションを検出し、RAM の枯渇を招くことなくメモリを分散するために必要な手順を実行することです。
- デバイス ドライバーに関連した問題:ドライバーでメモリ割り当て関数が誤って呼び出されると、デバイス ドライバーによってすべてのプロセスのワーキング セットのページングが発生する可能性があります。
- オペレーション システムに関連した問題

以下では、これらの各カテゴリに関する情報を確認できます。

- **アプリケーションに関連した問題**:アプリケーションによってシステム上のすべての RAM が消費される場合があります。 メモリに対して新しい要求が行われた場合、OS ではそれらを満たそうとし、空きメモリがない場合は、実行中のアプリケーションのワーキング セットがメモリ要求を満たすようにトリミングされます。 このような場合、すべてのアプリケーションではないにしてもほとんどのワーキング セットで大幅に減少するのが見られる可能性があります。 これを確認するには、システム上のすべてのアプリケーションの次のパフォーマンス モニター カウンターを収集します。

  - パフォーマンス オブジェクト:Process
  - カウンター:Working Set
  
  また、次のカウンターを監視して、システムで使用できる物理メモリの量を関連付けます。
  
  - パフォーマンス オブジェクト:メモリ
  - カウンター:使用可能なメモリ (MB)
  
  見られる可能性がある典型的な動作として、使用可能なメモリが 0 MB 近くにまで減ると同時に、システム上のほとんど (すべて) のワーキング セット カウンターが突然減少することが挙げられます。 このような動作が見られる場合は、SQL Server の最大サーバー メモリを減らすことなど、システムのメモリ使用量を減らすための手順を実行する必要があることがあります。
  
    また、アプリケーションでシステム キャッシュが過剰に使用され、システム キャッシュが大量に増大する可能性があります。 システム キャッシュの増加に対応するために、システムでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスまたは他のアプリケーションのワーキング セットをページ アウトします。 この問題が発生した場合は、アプリケーション内でいくつかのメモリ管理関数を使用できます。 これらの関数により、アプリケーション内のファイル I/O 操作で使用できるシステム キャッシュ領域が制御されます。 たとえば、SetSystemFileCacheSize 関数と GetSystemFileCacheSize 関数を使用すると、ファイル I/O 操作で使用できるシステム キャッシュ領域を制御できます。
  
    メモリ パフォーマンス オブジェクトを使用すると、このオブジェクト内のさまざまなカウンターの値を表示して、システム キャッシュのワーキング セットで使用されているメモリが多すぎるかどうかを判断できます。 たとえば、Cache Bytes カウンターと System Cache Resident Bytes カウンターを表示できます。 このトピックの詳細については、以下を参照してください。
  
    - [キャッシュが多すぎる](/archive/blogs/ntdebugging/too-much-cache)
    - [Microsoft Windows Dynamic Cache Service](/archive/blogs/ntdebugging/microsoft-windows-dynamic-cache-service)
    - [システム ファイルのキャッシュで物理 RAM の大部分が使用されると、アプリケーションおよびサービスでパフォーマンスの問題が発生する](https://support.microsoft.com/help/976618)
  
    "Microsoft Windows Dynamic Cache Service" をダウンロードして展開すると、システム キャッシュによって使用されるメモリを制御できます。

- **デバイス ドライバーに関連した問題**:デバイス ドライバーで `MmAllocateContiguousMemory` 関数が使用され、HighestAcceptableAddress パラメーターの値が 4 ギガバイト (GB) 未満に設定されている場合、Windows オペレーティング システムによって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスを含む、システム上のプロセスのワーキング セットがページ アウトされることがあります。 この問題を解決するには、ドライバーの更新プログラムについて、デバイス ドライバーの製造元に問い合わせてください。

    デバイス ドライバーでメモリの割り当てが試行されると、Windows オペレーティング システムによって、他のアプリケーションのワーキング セットがページ アウトされることがあります。 この Windows 修正プログラムにより、イベント トレースを使用して、問題の原因となっているデバイス ドライバーを見つけることができます。 ワーキング セットのトリミング動作を引き起こす特定のドライバーの詳細については、「[連続するメモリを割り当てるドライバーの識別](/previous-versions/windows/desktop/xperf/identifying-drivers-that-allocate-contiguous-memory)」を参照してください。

- **オペレーティング システムに関連した問題**:Windows オペレーティング システムによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスのワーキング セットがページ アウトされる原因となっている既知の問題を解決するには、次の Microsoft サポート技術情報の記事で説明されている修正プログラムを適用します。

  > [!NOTE]
  > 修正プログラムは累積されます。 新しいバージョンの修正プログラムには、以前のバージョンの修正プログラムが含まれています。

  - システムでいくつかの高度な TCP 機能が使用されている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットはトリミングされる可能性があります。 詳細については、[RSS や NetDMA などの高度なネットワーク パフォーマンス機能のトラブルシューティング方法](/troubleshoot/windows-server/networking/troubleshoot-network-performance-features-rss-netdma)に関するページを参照してください。

  - Windows Server 2008 で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行している場合は、他のオペレーティング システムのコンポーネントによるワーキング セットのトリミングまたは不必要に過剰なメモリの消費につながる可能性がある既知の問題について、修正プログラムを適用する必要があります。 詳細については、[Active Directory 診断テンプレートを使用して Perfmon.exe を実行し、Windows Server 2008 ベースのドメイン コントローラーでレポートを生成すると、レポート生成プロセスが応答しなくなる場合がある](/troubleshoot/windows-server/performance/report-generation-process-stops-responding)問題に関する記事を参照してください。

  - Windows Server 2008 R2 で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行している場合は、作業セットのトリミングにつながる可能性がある既知の問題に対する修正プログラムを適用する必要があります。 詳細については、次の記事を参照してください。

    - [大規模なアプリケーションを実行すると、Windows 7 または Windows Server 2008 R2 を実行しているコンピューターが応答しなくなる](https://support.microsoft.com/help/979149)
    - [NUMA ベースのプロセッサが搭載されており、かつ Windows Server 2008 R2 または Windows 7 が実行されているコンピューターで、あるスレッドによって最初の 4 GB のメモリ内で大量のメモリが要求された場合に、パフォーマンスが低下する](https://support.microsoft.com/help/2155311)
    - [Windows Server 2008 R2 で Storport ドライバーが使用されていると、コンピューターのパフォーマンスが断続的に低下したり、応答しなくなったりする](https://support.microsoft.com/help/2468345)

## <a name="important-considerations-before-you-assign-the-lock-pages-in-memory-user-right"></a>"Lock pages in memory" ユーザー権利を割り当てる前の重要な考慮事項

Lock pages in memory ユーザー権利を割り当てる前に、追加で考慮する必要があります。 正しく構成されていないシステムにこのユーザー権利を割り当てると、システムが不安定になったり、システム全体のパフォーマンスが低下したりする場合があります。 さらに、イベント ログにイベント ID 333 が記録される場合があります。

これらの問題について Microsoft カスタマー サポート サービス (CSS) に問い合わせると、CSS エンジニアが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの開始アカウントとして使用されているユーザー アカウントに対して、このユーザー権利の取り消しを求めることがあります。 この手順は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] やシステムで実行されている他のアプリケーションに必要なさまざまなオプションの構成に CSS エンジニアが使用できる重要なパフォーマンス データを収集するために必要な場合があります。 CSS エンジニアがパフォーマンス データを収集した後に、Lock pages in memory ユーザー権利を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの開始アカウントに割り当てることができます。

Lock pages in memory ユーザー権利を割り当てる前に、パフォーマンス モニターのログをキャプチャして、システムにインストールされているさまざまなアプリケーションやサービスのメモリ要件を確認してください。 これらのアプリケーションには、SQL Server も含まれます。 メモリ要件を特定するには、次のベースライン情報を収集します。

- max server memory オプションと min server memory オプションが正しく設定されていることを確認してください。 これらのオプションには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスのバッファー プールのメモリ要件のみが反映されます。 これらのオプションには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス内の他のコンポーネント用に割り当てられたメモリは含まれません。 これらのコンポーネントには、次のものが含まれます。

  - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ワーカー スレッド
  - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスのアドレス空間の内部に読み込まれる各種 DLL やコンポーネント
  - バックアップ操作と復元操作

- DLL およびコンポーネントには、さまざまな OLE DB プロバイダー、拡張ストアド プロシージャのほか、sp_OACreate ストアド プロシージャ、リンク サーバー、および CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用される Microsoft COM のオブジェクトが含まれます。 これらのコンポーネントに割り当てられるメモリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスのアドレス空間の非バッファー プール領域に分類されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス全体で使用できる理想的なメモリの最大量を判断するには、バッファー プールを使用しないコンポーネントに割り当てられたメモリを、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで使用するメモリの合計から減算する必要があります。 その後、残りの値を使用して max server memory オプションを設定できます。 max server memory オプションと min server memory オプションを設定する前に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「メモリ オプションの手動設定」のトピックをよく確認してください。

- 他のアプリケーションと Windows オペレーティング システム コンポーネントのメモリ要件を決定します。 アプリケーションには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション エージェント、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Services、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フル テキスト検索など、他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントが含まれている場合があります。 バックアップ操作とファイル コピー操作が実行されるアプリケーションでは、大量のメモリを使用する場合があります。 一括コピーなどの操作やファイル IO を生成するスナップショット エージェントが考えられます。 max server memory オプションと min server memory オプションの値を決定するときは、これらすべてのアプリケーションのメモリ要件を考慮する必要があります。 各プロセスの Process オブジェクトの下にある Private Bytes カウンターと Working Set カウンターを使用して、特定のプロセスのメモリ要件を決定できます。

- 既定では、組み込みのローカル システム アカウントには、Lock pages in memory ユーザー権利が既に割り当てられています。 詳細については、次の Microsoft Web サイトを参照してください。[ローカル システムで Lock pages in memory の権限を割り当てる必要がありますか](https://techcommunity.microsoft.com/t5/sql-server-support/do-i-have-to-assign-the-lock-pages-in-memory-privilege-for-local/ba-p/315426?advanced=false&collapse_discussion=true&search_type=thread)

- ドメイン内のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで Windows ユーザー アカウントをグローバルに使用する場合は、グループ ポリシー構成を使用して割り当てられたユーザー権利を確認します。 32 ビットの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスでは、このアカウントを開始アカウントとして使用できます。 ただし、このアカウントには、`Address Windowing Extensions` (AWE) 機能を有効にするための Lock pages in memory ユーザー権利が必要です。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「SQL Server に対する最大メモリ容量の指定」のトピックを参照してください。

- max server memory オプションと min server memory オプションを複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して構成する前に、SQL Server の各インスタンスに対する非バッファー プールのメモリ要件を考慮してください。 次に、SQL Server の各インスタンスに対してこれらのオプションを構成します。

このベースライン情報は、負荷がピークの間に収集するのが理想的です。 それによって、さまざまなアプリケーションおよびコンポーネントの、ピーク時の負荷に対応するメモリ要件を確認できます。 メモリ要件は、システム上で実行されているアクティビティやアプリケーションによって、システムごとに異なります。 動的管理ビュー sys.dm_os_process_memory で提供されている情報を照会して、そのシステムでメモリ不足の状態が発生しているかどうかを把握できます。 詳細については、「[sys.dm_os_process_memory (Transact-SQL)](../system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md)」を参照してください。

## <a name="improvements-added-in-windows-server-2008-and-r2-version"></a>Windows Server 2008 および R2 バージョンで追加された機能強化

Windows Server 2008 および Windows Server 2008 R2 では、連続するメモリ割り当てメカニズムが向上しています。 この機能強化により、Windows Server 2008 と Windows Server 2008 R2 では、新しいメモリ要求が到着したときに、アプリケーションによってワーキング セットがページ アウトされることによる影響を減らすことができます。

次に示すのは、Microsoft のホワイトペーパー「Windows でのメモリ管理の進歩」からの本機能強化に関する説明です。

"*Windows Server 2008 では、物理的に連続するメモリ割り当てが大幅に強化されています。一般的にワーキング セットをトリミングしたり I/O 操作を実行したりすることなく、メモリ マネージャーでページが動的に置き換えられるようになったため、連続するメモリ割り当て要求が成功する可能性がはるかに高くなっています。さらに、カーネル スタックやファイル システム メタデータ ページなど、他にも多くの種類のページが置換の候補になりました。その結果、より連続するメモリがいつでも一般的に利用できます。また、このような割り当てを取得するためのコストが大幅に削減されています。* "

詳細については、[SQL Server のワーキング セットのトリミングにおける問題点](https://techcommunity.microsoft.com/t5/sql-server-support/sql-server-working-set-trim-problems-consider/ba-p/315462?advanced=false&collapse_discussion=true&search_type=thread)に関するページを参照してください。

この記事で説明するサード パーティ製品は、Microsoft に関係のない企業によって製造されています。 Microsoft では、暗黙的またはそれ以外に関わらず、これらの製品のパフォーマンスや信頼性について何ら保証しません。