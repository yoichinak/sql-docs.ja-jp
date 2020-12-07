---
description: パラメーター化されたフィルター - パラメーター化された行フィルター
title: パラメーター化された行フィルター | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], dynamic filters
- merge replication [SQL Server replication], dynamic filters
- parameterized filters [SQL Server replication]
- filters [SQL Server replication], dynamic
- merge replication parameterized filters [SQL Server replication]
- publications [SQL Server replication], parameterized filters
- parameterized filters [SQL Server replication], about parameterized filters
- filters [SQL Server replication], parameterized
- dynamic filters [SQL Server replication]
ms.assetid: b48a6825-068f-47c8-afdc-c83540da4639
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 656f36cce2c1b458f2eb85c734709691b59a82bf
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88423546"
---
# <a name="parameterized-filters---parameterized-row-filters"></a>パラメーター化されたフィルター - パラメーター化された行フィルター
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  パラメーター化された行フィルターを使用すると、複数のパブリケーションを作成しなくても、パーティションの異なるデータを各サブスクライバーに送信できます (以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、パラメーター化されたフィルターは動的フィルターと呼ばれていました)。 パーティションとは、テーブル内の行のサブセットのことです。パラメーター化された行フィルターの作成時に選択した設定に基づき、パブリッシュされたテーブルの各行は、1 つのパーティションのみに属するか (重複しないパーティションが作成されます)、2 つ以上のパーティションに属します (重複するパーティションが作成されます)。  
  
 重複しないパーティションは、サブスクリプション間で共有するか、または 1 つのサブスクリプションのみが特定のパーティションを受け取るように制限することができます。 パーティションの動作を制御する設定については、このトピックの「適切なフィルター選択オプションの使用」で説明します。 これらの設定を使用すると、アプリケーションおよびパフォーマンスの要件に応じて、パラメーター化されたフィルター選択を調整できます。 一般に、重複するパーティションを使用すると柔軟性が向上し、重複しないパーティションを単一のサブスクリプションにレプリケートするとパフォーマンスが向上します。  
  
 パラメーター化されたフィルターは単一のテーブルで使用し、通常は関連するテーブルに対するフィルター選択を拡張するために結合フィルターと組み合わせて使用します。 詳しくは、「 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)」をご覧ください。  
  
 パラメーター化された行フィルターを定義または変更するには、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」を参照してください。  
  
## <a name="how-parameterized-filters-work"></a>パラメーター化されたフィルターの動作  
 パラメーター化された行フィルターでは、WHERE 句を使用して、パブリッシュする適切なデータを選択します。 静的行フィルターのようにこの句でリテラル値を指定するのではなく、システム関数 SUSER_SNAME() および HOST_NAME() のいずれかまたは両方を指定します。 ユーザー定義関数も使用できますが、その場合はユーザー定義関数の本体に SUSER_SNAME() または HOST_NAME() を含めるか、または `MyUDF(SUSER_SNAME()`のように、ユーザー定義関数でこれらのシステム関数のいずれかを評価する必要があります。 ユーザー定義関数の本体に SUSER_SNAME() または HOST_NAME() を含める場合、その関数にパラメーターを渡すことはできません。  
  
 システム関数 SUSER_SNAME() および HOST_NAME() は、マージ レプリケーションに固有のものではありませんが、パラメーター化されたフィルター選択のためにマージ レプリケーションで使用されます。  
  
-   SUSER_SNAME() は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスに対する接続のログイン情報を返します。 この関数をパラメーター化されたフィルターで使用した場合、マージ エージェントがパブリッシャーに接続するために使用するログインが返されます (ログインはサブスクリプションを作成するときに指定します)。  
  
-   HOST_NAME() は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスに接続しているコンピューターの名前を返します。 この関数をパラメーター化されたフィルターで使用した場合、既定では、マージ エージェントが実行されているコンピューターの名前が返されます。 プル サブスクリプションの場合はサブスクライバーの名前になり、プッシュ サブスクリプションの場合はディストリビューターの名前になります。  
  
     サブスクライバーまたはディストリビューターの名前以外の値で、この関数をオーバーライドすることも可能です。 通常、アプリケーションでは、販売員の名前や ID など、より具体的な意味のある値でこの関数をオーバーライドします。 詳細については、このトピックの「HOST_NAME() 値のオーバーライド」を参照してください。  
  
 システム関数によって返された値は、フィルター選択しているテーブルで指定した列と比較され、適切なデータがサブスクライバーにダウンロードされます。 この比較は、サブスクリプションが初期化されたときに実行され (これにより初期スナップショットには適切なデータのみが含まれます)、またサブスクリプションが同期されるたびに実行されます。 既定では、パブリッシャーでの変更によってパーティションから行が移動すると、その行はサブスクライバーで削除されます (この動作は、[sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) の `@allow_partition_realignment` パラメーターを使用して制御されます)。  
  
> [!NOTE]  
>  パラメーター化されたフィルターの比較が実行されるときは、常にデータベース照合順序が使用されます。 たとえば、データベース照合順序で大文字と小文字が区別されず、テーブルまたは列の照合順序で大文字と小文字が区別される場合、比較では大文字と小文字は区別されません。  
  
### <a name="filtering-with-suser_sname"></a>SUSER_SNAME() によるフィルター選択  
 **サンプル データベースの** Employee テーブル [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] について考えてみます。 このテーブルには **LoginID** 列が含まれており、この列には各従業員のログインが '*domain\login*' という形式で格納されています。 このテーブルにフィルターを適用して、従業員が各自に関連するデータのみを受け取れるようにするには、フィルター句を次のように指定します。  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 たとえば、ある従業員の値が 'adventure-works\john5' であるとします。 マージ エージェントはパブリッシャーに接続するときに、サブスクリプションの作成時に指定されたログインを使用します (この場合は 'adventure-works\john5')。 次に、マージ エージェントは SUSER_SNAME() によって返された値をこのテーブル内の値と比較し、 **LoginID** 列に 'adventure-works\john5' という値が格納された行のみをダウンロードします。  
  
### <a name="filtering-with-host_name"></a>HOST_NAME() によるフィルター選択  
 **HumanResources.Employee** テーブルについて考えてみます。 このテーブルに、 **ComputerName** という列が含まれており、この列に各従業員のコンピューターの名前が '*name_computertype*' という形式で格納されているとします。 このテーブルにフィルターを適用して、従業員が各自に関連するデータのみを受け取れるようにするには、フィルター句を次のように指定します。  
  
```  
ComputerName = HOST_NAME()  
```  
  
 たとえば、ある従業員の値が 'john5_laptop' であるとします。 マージ エージェントはパブリッシャーに接続すると、HOST_NAME() によって返された値をこのテーブル内の値と比較し、 **ComputerName** 列に 'john5_laptop' という値が格納された行のみをダウンロードします。  
  
 フィルターでは関数を組み合わせて使用することもできます。 たとえば、従業員が自分のコンピューターで自分のログインを使用している場合にのみデータを受け取れるようにするには、フィルター句を次のように指定します。  
  
```  
LoginID = SUSER_SNAME() AND ComputerName = HOST_NAME()  
```  
  
 HOST_NAME() の値をオーバーライドしている場合を除き、HOST_NAME() によるフィルター選択は、通常はプル サブスクリプションでのみ使用します。 この関数によって返される値は、マージ エージェントが実行されているコンピューターの名前です。 この値は、プル サブスクリプションの場合は各サブスクリプションによって異なりますが、プッシュ サブスクリプションの場合は同じです (プッシュ サブスクリプションの場合、すべてのマージ エージェントがディストリビューターで実行されます)。  
  
> [!IMPORTANT]  
>  HOST_NAME() 関数の値はオーバーライドされている場合があります。したがって、HOST_NAME() を含むフィルターを使用してデータのパーティションへのアクセスを制御することはできません。 データのパーティションへのアクセスを制御するには、SUSER_SNAME()、SUSER_SNAME() と HOST_NAME() の組み合わせ、または静的行フィルターを使用します。  
  
#### <a name="overriding-the-host_name-value"></a>HOST_NAME() 値のオーバーライド  
 既に述べたとおり、HOST_NAME() は、既定では [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスに接続しているコンピューターの名前を返します。 パラメーター化されたフィルターを使用する場合、サブスクリプションの作成時に値を指定することによって、この値をオーバーライドすることがよくあります。 これにより、HOST_NAME() 関数は、コンピューターの名前ではなく、指定された値を返します。  
  
> [!NOTE]  
>  HOST_NAME() をオーバーライドした場合、HOST_NAME() 関数のすべての呼び出しは、指定された値を返します。 他のアプリケーションが、コンピューター名を返す HOST_NAME() 関数に依存していないことを確認してください。  
  
 **HumanResources.Employee** テーブルについて考えてみます。 このテーブルには **EmployeeID** という列があります。 このテーブルにフィルターを適用して各従業員が関連データのみを受け取れるようにするには、フィルター句を次のように指定します。  
  
 `EmployeeID = CONVERT(int,HOST_NAME())`  
  
 たとえば、従業員の Pamela Ansman-Wolfe には、280 という従業員 ID が割り当てられています。 この従業員のサブスクリプションの作成時に、従業員 ID の値 (この場合は 280) を HOST_NAME() 値に指定します。 マージ エージェントはパブリッシャーに接続すると、HOST_NAME() によって返された値をこのテーブル内の値と比較し、 **EmployeeID** 列に 280 という値が格納された行のみをダウンロードします。  
  
> [!IMPORTANT]
>  HOST_NAME() 関数は **nchar** 型の値を返します。したがって、上記の例のようにフィルター句の列が数値データ型の場合は、CONVERT を使用する必要があります。 `CONVERT(nchar,EmployeeID) = HOST_NAME()`のように、パラメーター化された行フィルターの句で列名に関数を適用するとパフォーマンスが低下するため、使用しないことをお勧めします。 代わりに、この例で示されている `EmployeeID = CONVERT(int,HOST_NAME())`という句を使用することをお勧めします。 この句は、[sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) の `@subset_filterclause` パラメーターに使用できますが、通常はパブリケーションの新規作成ウィザードでは使用できません (このウィザードではフィルター句を実行して検証が行われますが、コンピューター名を **int** に変換できないので、失敗します)。 パブリケーションの新規作成ウィザードを使用する場合は、このウィザードで `CONVERT(nchar,EmployeeID) = HOST_NAME()` を指定し、次に [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を使用して句を `EmployeeID = CONVERT(int,HOST_NAME())` に変更してから、パブリケーションのスナップショットを作成することをお勧めします。  
  
 **HOST_NAME() 値をオーバーライドするには**  
  
 以下のいずれかの方法で、HOST_NAME() 値をオーバーライドします。  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: サブスクリプションの新規作成ウィザードの **HOST\_NAME\(\) 値** ページで値を指定します。 サブスクリプションの作成については、「[パブリケーションのサブスクライブ](../../../relational-databases/replication/subscribe-to-publications.md)」を参照してください。  
  
-   レプリケーション [!INCLUDE[tsql](../../../includes/tsql-md.md)] プログラミング: (プッシュ サブスクリプション用に) [sp_addmergesubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) または、(プル サブスクリプション用に) [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) の `@hostname` パラメーターの値を指定します。  
  
-   マージ エージェント: コマンド ラインまたはエージェント プロファイルで **-Hostname** パラメーターの値を指定します。 マージ エージェントの詳細については、「 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)」を参照してください。 エージェント プロファイルの詳細については、「 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)」を参照してください。  
  
## <a name="initializing-a-subscription-to-a-publication-with-parameterized-filters"></a>パラメーター化されたフィルターを使用したパブリケーションへのサブスクリプションの初期化  
 パラメーター化された行フィルターがマージ パブリケーションで使用される場合、レプリケーションは 2 つの要素から成るスナップショットを持つ各サブスクリプションを初期化します。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
## <a name="using-the-appropriate-filtering-options"></a>適切なフィルター選択オプションの使用  
 パラメーター化されたフィルターを使用する場合、制御できる主要な要素が 2 つあります。  
  
-   マージ レプリケーションによるフィルターの処理方法。" **パーティション グループを使用** " および " **パーティションの変更を保持**" の 2 つのパブリケーション設定のいずれかで制御されます。  
  
-   サブスクライバー間でのデータの共有方法。アーティクル設定の **[パーティションのオプション]** で指定する必要があります。  
  
 フィルター選択オプションを設定するには、「 [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)」を参照してください。  
  
### <a name="setting-use-partition-groups-and-keep-partition-changes"></a>"パーティション グループを使用" および "パーティションの変更を保持" の設定  
 **パーティション グループを使用** オプションと **パーティションの変更を保持** オプションでは、いずれもパブリケーション データベースに追加のメタデータを格納することにより、フィルター選択されたアーティクルを持つパブリケーションの同期パフォーマンスを向上します。 **パーティション グループを使用** オプションでは、事前計算済みパーティション機能を使用することにより、パフォーマンスを向上させることができます。 このオプションは、パブリケーションのアーティクルが一連の要件を満たしている場合に、既定で **true** に設定されています。 これらの要件の詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。 アーティクルが事前計算済みパーティションを使用するための要件を満たしていない場合は、 **パーティションの変更を保持** オプションが **true** に設定されます。  
  
### <a name="setting-partition-options"></a>[パーティションのオプション] の設定  
 **[パーティションのオプション]** プロパティの値は、アーティクルを作成するときに、フィルター選択されたテーブルのデータをサブスクライバーが共有する方法に応じて設定します。 このプロパティは、 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)、 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)、および **[アーティクルのプロパティ]** ダイアログ ボックスを使用して、4 つの値のいずれかに設定できます。 このプロパティは、 **[フィルターの追加]** ダイアログ ボックスまたは **[フィルターの編集]** ダイアログ ボックスを使用して、2 つの値のいずれかに設定できます。これらのダイアログ ボックスは、パブリケーションの新規作成ウィザードおよび **[パブリケーションのプロパティ]** ダイアログ ボックスから使用できます。 次の表は、利用可能な値をまとめたものです。  
  
|説明|[フィルターの追加] および [フィルターの編集] の値|[アーティクルのプロパティ] の値|ストアド プロシージャ内の値|  
|-----------------|-----------------------------------------|---------------------------------|--------------------------------|  
|パーティション内のデータは重複しています。サブスクライバーはパラメーター化されたフィルターで参照されている列を更新できます。|**[このテーブルの 1 行を複数のサブスクリプションに移動する]**|**[重複する]**|**0**|  
|パーティション内のデータは重複しています。サブスクライバーはパラメーター化されたフィルターで参照されている列を更新できません。|なし*|**[重複する (パーティション外のデータ変更を禁止)]**|**1**|  
|パーティション内のデータは重複していません。データはサブスクリプション間で共有されます。 サブスクライバーはパラメーター化されたフィルターで参照されている列を更新できません。|なし*|**[重複しない (複数のサブスクリプションで共有)]**|**2**|  
|パーティション内のデータは重複していません。パーティションごとに単一のサブスクリプションが存在します。 サブスクライバーはパラメーター化されたフィルターで参照されている列を更新できません。**|**[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]**|**[重複しない (単一のサブスクリプション)]**|**3**|  
  
 \*基になるフィルター選択オプションが **0**、**1**、または **2** に設定されている場合、**[フィルターの追加]** ダイアログ ボックスと **[フィルターの編集]** ダイアログ ボックスには、**[このテーブルの 1 行を複数のサブスクリプションに移動する]** が表示されます。  
  
 **このオプションを指定する場合、該当するアーティクル内のデータの各パーティションに対し、単一のサブスクリプションのみを使用できます。 第 2 のサブスクリプションを作成し、その新しいサブスクリプションのフィルター選択条件が既存のサブスクリプションと同じパーティションとして判別される場合、既存のサブスクリプションは削除されます。  
  
> [!IMPORTANT]  
>  **[パーティションのオプション]** の値は、サブスクライバーによるデータの共有方法に応じて設定する必要があります。 たとえば、パーティションが重複せず、パーティションごとに単一のサブスクリプションが存在するように指定したにもかかわらず、データが別のサブスクライバーで更新された場合、マージ エージェントは同期中に失敗し、未集約が発生することがあります。  
  
#### <a name="selecting-the-appropriate-partition-option"></a>適切なパーティション オプションの選択  
 重複しないパーティションは事前計算済みパーティションと連動して、一部の機能上の制限が許容される状況でパフォーマンスを向上します。 事前計算済みパーティションを使用すると、サブスクライバーへのダウンロードの速度は向上しますが、アップロードの速度は低下します。 重複しないパーティションを使用すると、事前計算済みパーティションに関連するアップロードの負荷は最小限に抑えられます。 重複しないパーティションのパフォーマンス上の利点は、使用するパラメーター化されたフィルターと結合フィルターが複雑になるほど明確になります。  
  
 パブリケーションで使用するパーティション オプションを決めるときは、次のシナリオを検討してください。  
  
-   [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] には移動営業部門があり、郵便番号ごとに顧客の担当が決まっています。 アプリケーションでは、顧客がある営業区域から別の営業区域に移動した場合に、郵便番号を更新し、その顧客が別の営業担当者に割り当てられるようにする必要があります。 パラメーター化されたフィルターは顧客の郵便番号に基づいています。更新により、該当する郵便番号が、ある営業担当者のパーティションから削除されて別の営業担当者のパーティションに挿入されます。 このためには、パラメーター化されたフィルターで参照されている列を更新する機能を持つ、重複するパーティションが必要です。 このオプションでは、柔軟性は最大になりますが、重複しないパーティションほどのパフォーマンスは得られない可能性があります。  
  
-   ある人材紹介会社では、州の各郡にある地域事務所にデータを提供しています。 このデータは重複していません。この会社の本社にあるテーブルの各行は、1 つのパーティションにのみ含まれていますが、そのパーティションは同じ郡にある複数の事務所に送信されます。 この場合、サブスクリプション間で共有されるパーティションに対して重複しないパーティション オプションを使用するのが適切です。これにより、重複するパーティションよりも高いパフォーマンスを実現しつつ、アプリケーションの要件を満たすことができます。  
  
-   重複しないパーティションを使用し、1 つのサブスクリプションだけが 1 つのパーティション内のデータを受信および更新する場合は、さらにパフォーマンスを向上させることができます。 このシナリオは、POS システムや、データが主にサブスクライバーで収集されてパブリッシャーにアップロードされるフィールド フォース アプリケーションで一般的です。 配送アプリケーションの **Package** テーブルについて考えてみます。各配送物がトラックに積み込まれると、その配送物の状態が **Package** テーブルで変更され、変更が本部にレプリケートされます。 別のトラックの運転手が同じ配送物の状態を更新することはありません。したがって **Package** テーブルには、パーティションごとに単一のサブスクリプションが存在する重複しないパーティションが適しています。  
  
#### <a name="considerations-for-nonoverlapping-partitions"></a>重複しないパーティションに関する注意点  
 重複しないパーティションを使用するときは、以下の点に注意してください。  
  
##### <a name="general-considerations"></a>一般的な考慮事項  
  
-   パブリケーションでは事前計算済みパーティションを使用する必要があります。  
  
-   1 つの行は 1 つのパーティションにのみ属している必要があります。  
  
-   アーティクルを論理レコードの一部にすることはできません。  
  
-   代替同期パートナーはサポートされません (この機能は非推奨とされます)。  
  
-   サブスクライバーはパラメーター化されたフィルターで参照されている列を更新できません。  
  
-   サブスクライバーでの挿入がパーティションに属さない場合、その挿入は削除されません。 ただし、他のサブスクライバーにはレプリケートされません。  
  
-   重複するパーティションを使用する一部の状況では、マージ エージェントがデータを挿入するときに、ID 範囲が調整されます。 重複しないパーティションでは、サブスクリプション データベースで ID 範囲を調整する権限を持つユーザーのみが、挿入時に範囲を調整できます。 ユーザーはテーブルを所有しているか、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、または **db_ddladmin** 固定データベース ロールのメンバーである必要があります。  
  
##### <a name="additional-considerations-for-nonoverlapping-partitions-with-a-single-subscription-per-partition"></a>パーティションごとに単一のサブスクリプションが存在する重複しないパーティションに関するその他の注意点  
  
-   アーティクルは 1 つのパブリケーションにのみ存在することができます。アーティクルを再パブリッシュすることはできません。  
  
-   パブリケーションでは、サブスクライバーによるスナップショット処理の開始を許可する必要があります。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
##### <a name="additional-considerations-for-join-filters"></a>結合フィルターに関するその他の注意点  
  
-   結合フィルター階層では、重複するパーティションのアーティクルを、重複しないパーティションのアーティクルよりも上位にすることはできません。 つまり、子アーティクルで重複しないパーティションを使用する場合、親アーティクルでも重複しないパーティションを使用する必要があります。 結合フィルターの詳細については、「 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)」を参照してください。  
  
-   重複しないパーティションを子に持つ結合フィルターでは、 **一意キーの結合** プロパティを 1 に設定する必要があります。 詳しくは、「 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)」をご覧ください。  
  
-   アーティクルは、1 つのパラメーター化されたフィルターまたは結合フィルターのみを持っている必要があります。 パラメーター化されたフィルターを持ち、かつ結合フィルターの親になることは可能です。 パラメーター化されたフィルターを持ち、かつ結合フィルターの子になることはできません。 複数の結合フィルターを持つことはできません。  
  
-   パブリッシャーの 2 つのテーブルに結合フィルター リレーションシップがあり、子テーブルの行が親テーブルの行と対応していない場合、その行を親テーブルに挿入しても、関連する行はサブスクライバーにダウンロードされません (行は重複するパーティションによってダウンロードされます)。 たとえば、 **SalesOrderDetail** テーブルの行に対応する行が **SalesOrderHeader** テーブル内に存在せず、その行を **SalesOrderHeader** に挿入した場合、その行はサブスクライバーにダウンロードされますが、 **SalesOrderDetail** 内の対応する行はダウンロードされません。  
  
## <a name="see-also"></a>参照  
 [時間ベースの行フィルターの推奨事項](../../../relational-databases/replication/merge/best-practices-for-time-based-row-filters.md)   
 [パブリッシュされたデータのフィルター処理](../../../relational-databases/replication/publish/filter-published-data.md)   
 [マージ レプリケーション用にパブリッシュされたデータのフィルター選択](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
