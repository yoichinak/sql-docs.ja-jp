---
title: フェールオーバー クラスター インスタンスのアップグレード
description: インストール メディアを使用して SQL Server Always On フェールオーバー クラスター インスタンスをアップグレードする手順。 ローリング アップグレード、およびマルチサブネット クラスターのアップグレードについて説明します。
ms.custom: seo-lt-2019
ms.date: 11/21/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover cluster instances
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: cawrites
ms.author: chadam
ms.openlocfilehash: cad44bde76e3915aeb5f99d8eeb415d89b02359e
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127582"
---
# <a name="upgrade-a-failover-cluster-instance"></a>フェールオーバー クラスター インスタンスのアップグレード 
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを、新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]バージョン、新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]サービス パック、または累積更新プログラムにアップグレードするか、新しい Windows サービス パックや累積更新プログラムを、すべてのフェールオーバー クラスター ノードに個別にインストールして、ダウンタイムを、単一の手動フェールオーバー (元のプライマリにフェールバックする場合は、2 回の手動フェールオーバー) に制限できます。  

  
 フェールオーバー クラスター インスタンスを含むノードの Windows Server オペレーティング システムのアップグレードは、[!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] より前のオペレーティング システムではサポートされません。 [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] 以降で実行されている Windows Server クラスター ノードのアップグレードについては、「[ローリング アップグレードまたは更新の実行](#perform-a-rolling-upgrade-or-update)」を参照してください。  
  
 サポートの詳細は、次のとおりです。  
  
-   ユーザー インターフェイスとコマンド プロンプトの両方からの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アップグレードがサポートされています。 各フェールオーバー クラスター ノードでコマンド プロンプトからアップグレードを実行するか、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ UI を使用して各クラスター ノードをアップグレードできます。 詳細については、次を参照してください。

   - 新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスを作成する
   - [コマンド プロンプトからの SQL Server のインストール](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

-   次のシナリオは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アップグレードではサポートされていません。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスからフェールオーバー クラスター インスタンスにはアップグレードできません。  
  
    -   フェールオーバー クラスター インスタンスに機能を追加することはできません。 たとえば、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のみの既存のフェールオーバー クラスター インスタンスに [!INCLUDE[ssDE](../../../includes/ssde-md.md)] を追加することはできません。  
  
    -   フェールオーバー クラスター インスタンスを、Windows Server フェールオーバー クラスターのいずれかのノードのスタンドアロン インスタンスにダウングレードすることはできません。  
  
    -   フェールオーバー クラスター インスタンスのエディションの変更は、特定のシナリオに制限されています。 詳細については、「 [サポートされているバージョンとエディションのアップグレード](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)」をご覧ください。  
  
-   フェールオーバー クラスター インスタンスのアップグレードにおけるダウンタイムは、フェールオーバー時間およびアップグレード スクリプトの実行に必要な時間のみです。 次のフェールオーバー クラスター インスタンスのローリング アップグレード プロセスに従い、さらに、すべてのノードですべての前提条件を満たしてから、アップグレード プロセスを開始すると、ダウンタイムを最小限に抑えることができます。 メモリ最適化テーブルを使用している場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をアップグレードすると、余分な時間がかかることがあります。 詳細については、「 [データベース エンジンのアップグレード計画の策定およびテスト](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)」を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
 作業を開始する前に、次の重要な情報を確認してください。  
  
-   [サポートされているバージョンとエディションのアップグレード](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md):使用している Windows オペレーティング システムのバージョンと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のバージョンから [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] にアップグレードできることを確認します。 たとえば、SQL Server 2005 フェールオーバー クラスタリング インスタンスから [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] には直接アップグレードできません。また、[!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)] で実行されているフェールオーバー クラスター インスタンスをアップグレードすることもできません。  
  
-   [データベース エンジンのアップグレード方法の選択](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md):サポートされるバージョンとエディションのアップグレードを確認して、適切なアップグレードの方法と手順を選択します。また、環境にインストールされているその他のコンポーネントに基づいて、正しい順序でコンポーネントをアップグレードします。  
  
-   [データベース エンジンのアップグレード計画の策定およびテスト](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md):リリース ノート、アップグレードに関する既知の問題、アップグレード前のチェックリストを確認して、アップグレードの計画を作成およびテストします。  
  
-   [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] のインストールにおけるソフトウェア要件を確認します。 その他のソフトウェアが必要な場合は、ダウンタイムを最小限に抑えるために、アップグレード プロセスを開始する前に、各ノードにソフトウェアをインストールします。  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>ローリング アップグレードまたは更新の実行  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスを [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] にアップグレードするには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを使用して、フェールオーバー クラスター インスタンスに関与している各ノードをパッシブ ノードから 1 つずつアップグレードします。 各ノードをアップグレードすると、ノードはフェールオーバー クラスター インスタンスの実行可能な所有者から除外されます。 予期しないフェールオーバーが発生した場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のセットアップにより Windows Server クラスター ロールの所有権がアップグレード済みのノードに移動するまで、アップグレード済みのノードはフェールオーバーに関与しません。  
  
 既定では、アップグレード済みのノードにフェールオーバーする時期は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップにより自動的に決まります。 決定の際に基準になるのは、フェールオーバー クラスター インスタンス内のノード総数、およびアップグレード済みのノード数です。 ノード総数の半数以上がアップグレード済みの場合、次のノードでアップグレードする際、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップにより、アップグレード済みのノードにフェールオーバーが発生します。 アップグレード済みのノードにフェールオーバーする際、クラスター グループはアップグレード済みのノードに移動します。 すべてのアップグレード済みノードは実行可能な所有者の一覧に格納され、まだアップグレードされていないすべてのノードは実行可能な所有者の一覧から削除されます。 残りの各ノードをアップグレードすると、ノードはフェールオーバー クラスター インスタンスの実行可能な所有者に追加されます。  
  
 ダウンタイムでのこのプロセス結果は、1 回のフェールオーバー時間、および全フェールオーバー クラスター アップグレード時のデータベース アップグレード スクリプトの実行時間に限定されます。  
  
 アップグレード プロセス中にクラスター ノードのフェールオーバーの動作を制御するには、コマンド プロンプトでアップグレード操作を実行して、/FAILOVERCLUSTERROLLOWNERSHIP パラメーターを使用します。 詳細については、「 [コマンド プロンプトからの SQL Server のインストール](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)」を参照してください。  

 ## <a name="upgrade-with-installation-media"></a>インストール メディアを使用したアップグレード 
  
1.  アップグレードするエディションと一致するエディションの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール メディアで、ルート フォルダーの setup.exe をダブルクリックします。 必須コンポーネントがインストールされていない場合は、インストールするように求められます。  
  
2.  必須コンポーネントがインストールされると、インストール ウィザードによって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール センターが起動します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の既存のインスタンスをアップグレードするには、インスタンスを選択します。  
  
3.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ サポート ファイルが必要な場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップによってインストールされます。 コンピューターの再起動を求めるメッセージが表示されたら、再起動してから続行します。  
  
4.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 続行するには、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  [プロダクト キー] ページで、以前の製品バージョンのエディションに一致する新しいバージョンのエディション用の PID キーを入力します。 たとえば、エンタープライズ フェールオーバー クラスターをアップグレードするには、 [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]用の PID キーを入力する必要があります。 **[次へ]** をクリックして次に進みます。 フェールオーバー クラスターのアップグレードに使用する PID キーは、同じ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス内のすべてのフェールオーバー クラスター ノードで一貫している必要があります。  
  
6.  [ライセンス条項] ページで使用許諾契約書を読み、使用許諾条件に同意する場合は対応するチェック ボックスをオンにします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能向上に役立てるため、機能の使用状況オプションを有効にしてレポートを [!INCLUDE[msCoName](../../../includes/msconame-md.md)]に送信することもできます。 **[次へ]** をクリックして次に進みます。 セットアップを終了するには、 **[キャンセル]** をクリックします。  
  
7.  [インスタンスの選択] ページで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にアップグレードする [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]インスタンスを指定します。 **[次へ]** をクリックして次に進みます。  
  
8.  [機能の選択] ページでは、アップグレードする機能があらかじめ選択されています。 機能名を選択すると、右側のペインに各コンポーネント グループの説明が表示されます。 アップグレードする機能は変更できず、アップグレード操作中に機能を追加することもできないことに注意してください。 アップグレード操作の完了後に、アップグレードされた [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] のインスタンスに機能を追加するには、「 [SQL Server 2016 のインスタンスへの機能の追加 &#40;セットアップ&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)」を参照してください。  
  
     選択した機能の必須コンポーネントが、右側のペインに表示されます。 SQL Server セットアップでは、この手順の後半で説明するインストール手順の間に、まだインストールされていない必須コンポーネントをインストールします。 時間を節約するには、各ノードにこれらの必須コンポーネントを事前にインストールしておく必要があります。  
  
9. フィールドが [インスタンスの構成] ページで以前のインスタンスから自動的に生成されます。 新しい InstanceID 値を指定することもできます。  
  
     **[インスタンス ID]** : 既定では、インスタンス名がインスタンス ID として使用されます。 これは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 これは、既定のインスタンスの場合も名前付きインスタンスの場合も同様です。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、 **[インスタンス ID]** チェック ボックスをオンにして、値を指定します。 既定値をオーバーライドする場合、すべてのフェールオーバー クラスター ノードでアップグレードされたものと同じインスタンス ID を指定する必要があります。 アップグレード済みインスタンスのインスタンス ID は、すべてのノードに一致している必要があります。  
  
     **[検出されたインスタンスと機能]** : セットアップを実行中のコンピューター上にある [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスがグリッドに表示されます。 **[次へ]** をクリックして次に進みます。  
  
10. [必要なディスク領域] ページでは、指定した機能に必要なディスク領域が計算され、セットアップを実行中のコンピューター上の空き領域と比較されます。  
  
11. [フルテキスト検索アップグレード] ページで、アップグレードするデータベースのアップグレード オプションを指定します。 詳細については、「 [フルテキスト検索アップグレード オプション](../../../database-engine/install-windows/install-sql-server.md)」。  
  
12. **[エラー レポート]** ページで、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] に送信する、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能向上に役立つ情報を指定します。 既定では、エラー レポートのオプションは有効になっています。  
  
13. アップグレード処理が開始される前に、システム構成チェッカーによって別のルール セットが実行され、コンピューターの構成と指定した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能が検証されます。  
  
14. フェールオーバー クラスター インスタンス内のノードの一覧、および各ノードの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンポーネントのインスタンスのバージョン情報が [クラスター アップグレード レポート] ページに表示されます。 また、データベース スクリプト状態およびレプリケーション スクリプト状態が表示されます。 さらに、 **[次へ]** をクリックしたときの動作についての情報メッセージも表示されます。 アップグレード済みのフェールオーバー クラスター ノードの数とノード総数の違いに応じて、 **[次へ]** をクリックしたときの動作がセットアップにより表示されます。 必須コンポーネントをまだインストールしていない場合に生じ得る不要なダウンタイムについての警告も表示されます。   
  
15. [アップグレードの準備完了] ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 続行するには、 **[アップグレード]** をクリックします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップは、選択した機能の必須コンポーネントを最初にインストールし、その後で機能をインストールします。  
  
16. アップグレード中は、セットアップの進行に合わせてアップグレードの進行状況を監視できるように、[進行状況] ページに状態が表示されます。  
  
17. 現在のノードでアップグレードが終了すると、すべてのフェールオーバー クラスター ノード、各フェールオーバー クラスター ノードの機能、およびそのバージョン情報に関するアップグレード状態の情報が [クラスター アップグレード レポート] ページに表示されます。 表示されたバージョン情報を確認し、残りのノードでのアップグレードを続行します。 アップグレードしたノードでフェールオーバーが発生した場合は、状態ページを確認する作業も必要になります。 Windows クラスター アドミニストレーターのツールを使用して確認することもできます。  
  
18. アップグレードが終了すると、[完了] ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** をクリックします。  
  
19. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
20. アップグレード プロセスを完了するには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスの他のすべてのノードで、これらの手順を繰り返します。  
  
## <a name="upgrade-a-multi-subnet-failover-cluster-instance"></a>マルチサブネット フェールオーバー クラスター インスタンスをアップグレードする  

マルチサブネット環境で Always On フェールオーバー クラスター インスタンスをアップグレードするには、次の手順に従います。 
  
### <a name="to-upgrade-to-a-ssnoversion-multi-subnet-failover-cluster-instance-existing-ssnoversion-cluster-is-a-non-multi-subnet-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスター インスタンスにアップグレードするには (既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスターがマルチサブネット クラスターでない場合)  
  
1.  前述の手順に従って、フェールオーバー クラスター インスタンスをアップグレードします。  
  
2.  AddNode セットアップ アクションを使用して別のサブネット上に新しいノードを追加するには、 **[クラスター ネットワークの構成]** ページで IP アドレス リソースの依存関係が OR になっていることを確認します。 詳細については、[Always On フェールオーバー クラスター インスタンスでのノードの追加または削除 (セットアップ)](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md) に関するページを参照してください。  
  
### <a name="to-upgrade-a-multi-subnet-failover-cluster-instance-currently-using-stretch-vlan-to-use-multi-subnet"></a>現在、Stretch VLAN を使用しているマルチサブネット フェールオーバー クラスター インスタンスをアップグレードするには、マルチサブネットを使用します。  
  
1.  前述の手順に従って、クラスターを [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]にアップグレードします。  
  
2.  ネットワーク設定を変更し、リモート ノードを別のサブネットに移動します。  
  
3.  フェールオーバー クラスター マネージャーまたは PowerShell を使用して新しいサブネットに新しい IP アドレスを追加して、IP アドレス リソースの依存関係を OR に設定します。  
  
## <a name="next-steps"></a>次の手順  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]へのアップグレード後は、次の作業を実行します。  
  
-   [データベース エンジンのアップグレードの完了](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [データベース互換性モードの変更とクエリ ストアの使用](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [SQL Server 2016 の新機能を利用する](../../what-s-new-in-sql-server-2017.md)  
  

  
