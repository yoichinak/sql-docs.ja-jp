---
description: ID 列の管理
title: ID 列の管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 7d0a169e6b160bc865c5ba3c115803fb690cbe68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423486"
---
# <a name="manage-identity-columns"></a>ID 列の管理
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、ID 列を管理する方法について説明します。 サブスクライバー挿入がパブリッシャーにレプリケートされる場合、サブスクライバーとパブリッシャーに同じ ID 値が割り当てられないように、ID 列を管理する必要があります。 レプリケーションでは ID の範囲を自動的に管理することも、ID の範囲を手動で管理することもできます。  レプリケーションで使用できる ID 範囲管理オプションについては、「[ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
-   **ID 列を管理するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
  
-   複数のパブリケーションでテーブルをパブリッシュする場合、両方のパブリケーションに同じ ID 範囲管理オプションを指定する必要があります。 詳細については、「[データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)」の「複数のパブリケーションでのテーブルのパブリッシュ」を参照してください。  
  
-   複数のテーブルで使用できる自動的に増分する番号、またはテーブルを参照せずにアプリケーションから呼び出すことができる自動的に増分する番号を作成するには、「[シーケンス番号](../../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードの **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブで、ID 列の管理オプションを指定します。 このウィザードの使用の詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。 パブリケーションの新規作成ウィザードで選択した内容に応じて、次の操作を行います。  
  
-   **[パブリケーションの種類]** ページで **[マージ パブリケーション]** または **[更新可能なサブスクリプションを含むトランザクション パブリケーション]** を選択した場合は、ID 範囲の管理を自動または手動に設定します (自動 (既定値) に設定することを推奨します)。 このプロパティは、テーブルがパブリッシュされた後は変更できません。ただし、その他の関連プロパティは変更できます。  
  
-   他のパブリケーションの種類を選択した場合は、ID 範囲の管理を手動に設定する必要があります。  
  
 **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブで、ID 範囲としきい値を変更します。このダイアログ ボックスは、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスから開くことができます。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
#### <a name="to-specify-an-identity-column-management-option"></a>ID 列の管理オプションを指定するには  
  
1.  パブリッシャーが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]を実行している場合は、パブリケーションの新規作成ウィザードの **[パブリケーションの種類]** ページで、 **[マージ パブリケーション]** または **[更新可能なサブスクリプションを含むトランザクション パブリケーション]** を選択します。  
  
2.  **[アーティクル]** ページで、ID 列があるテーブルを選択します。  
  
3.  **[アーティクルのプロパティ]** をクリックしてから、 **[反転表示されたテーブル アーティクルのプロパティを設定]** をクリックします。  
  
4.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[ID 範囲の管理]** セクションで、 **[ID 範囲を自動的に管理します]** プロパティを **[自動]** または **[手動]** (パブリッシャーが [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降を実行している場合)、あるいは **[True]** または **[False]** (パブリッシャーが [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] よりも前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行している場合) に設定します。  
  
5.  手順 4. で **[自動]** または **[True]** を選択した場合は、次の表のオプションの値を入力します。 これらの設定の使用方法の詳細については、「[ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)」の「ID 範囲の割り当て」を参照してください。  
  
    |オプション|値|説明|  
    |------------|-----------|-----------------|  
    |**[パブリッシャーの範囲サイズ]**|範囲サイズの整数値 (たとえば 20000)。|「[ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)」の「ID 範囲の割り当て」を参照してください。|  
    |**[サブスクライバーの範囲サイズ]**|範囲サイズの整数値 (たとえば 10000)。|「[ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)」の「ID 範囲の割り当て」を参照してください。|  
    |**[範囲しきい値の割合]**|パーセントによるしきい値の整数値 (たとえば、90 は 90% を表します)。|ノードで使用されている ID 値全体の比率がこの値を超えると、新しい ID 範囲が割り当てられます。<br /><br /> <br /><br /> 注:この値の指定は必須ですが、この値は、キュー更新サブスクリプションを使用するサブスクライバーと、[!INCLUDE[ssEW](../../../includes/ssew-md.md)] または他のエディションの SQL Server の旧バージョンを実行しているマージ パブリケーションのサブスクライバーのみが使用します。 詳細については、「[ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)」の「ID 範囲の割り当て」を参照してください。|  
    |**[次の範囲の開始値]**|整数値。 読み取り専用です。|次の範囲はこの値から始まります。 たとえば、現在の範囲が 5001 ～ 6000 の場合、この値は 6001 になります。|  
    |**[最大 ID 値]**|整数値。 読み取り専用です。|ID 列の最大値です。 列の基本データ型によって決まります。|  
    |**Increment**|整数値。 読み取り専用です。|挿入のたびに ID 列の番号が増減する量。通常は 1 に設定されます。|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-modify-identity-ranges-and-thresholds-after-a-table-is-published"></a>テーブルがパブリッシュされた後に ID 範囲としきい値を変更するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで、ID 列があるテーブルを選択します。  
  
2.  **[アーティクルのプロパティ]** をクリックしてから、 **[反転表示されたテーブル アーティクルのプロパティを設定]** をクリックします。  
  
3.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[ID 範囲の管理]** セクションで、 **[パブリッシャーの範囲サイズ]** 、 **[サブスクライバーの範囲サイズ]** 、および **[範囲しきい値の割合]** プロパティの 1 つ以上に値を入力します。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 レプリケーション ストアド プロシージャを使用して、アーティクルを作成するときの ID 範囲管理オプションを指定できます。  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>トランザクション パブリケーションのアーティクルを定義する際に自動 ID 範囲管理を有効にするには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 パブリッシュするソース テーブルに ID 列がある場合、 **\@identityrangemanagementoption** に **auto** を指定し、パブリッシャーに割り当てる ID 値の範囲を **\@pub_identity_range** に、各サブスクライバーに割り当てる ID 値の範囲を **\@identity_range** に、新しい ID 範囲を割り当てる前に使用されていた ID 値の総数のパーセンテージを **\@threshold** に指定します。 アーティクルの定義の詳細については、「[Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」 (アーティクルの定義) を参照してください。  
  
    > [!NOTE]  
    >  ID 列のデータ型のサイズが、すべてのサブスクライバーに割り当てられる ID 範囲の総計をサポートできるだけの大きさであることを確認してください。  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>トランザクション パブリケーションのアーティクルを定義する際に自動 ID 範囲管理を無効にするには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 **\@identityrangemanagementoption** に **manual** を指定します。 アーティクルの定義の詳細については、「[Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」 (アーティクルの定義) を参照してください。  
  
2.  サブスクライバーの更新時に競合が発生しないように、サブスクライバーの ID アーティクル列に範囲を割り当てます。 詳細については、トピック「[ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)」で、手動による ID 範囲管理用に範囲を割り当てる方法に関する部分を参照してください。  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>マージ パブリケーションのアーティクルを定義する際の自動 ID 範囲管理を有効にするには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)を実行します。 パブリッシュするソース テーブルに ID 列がある場合、 **\@identityrangemanagementoption** に **auto** を指定し、サーバー サブスクリプションに割り当てる ID 値の範囲を **\@pub_identity_range** に、パブリッシャーおよび各クライアント サブスクリプションに割り当てる ID 値の範囲を **\@identity_range** に、新しい ID 範囲を割り当てる前に使用されていた ID 値の総数のパーセンテージを **\@threshold** に指定します。 いつ新しい ID 範囲が割り当てられるのかについては、「[ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)」の「ID 範囲の割り当て」を参照してください。 アーティクルの定義の詳細については、「[Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」 (アーティクルの定義) を参照してください。  
  
    > [!NOTE]  
    >  特にサーバー サブスクリプションを使用するサブスクライバーの場合、ID 列のデータ型のサイズが、すべてのサブスクライバーに割り当てられる ID 範囲の総計をサポートできるだけの大きさであることを確認してください。  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>マージ パブリケーションのアーティクルを定義する際に自動 ID 範囲管理を無効にするには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)を実行します。 次のいずれかの値を **\@identityrangemanagementoption** に指定します。  
  
    -   **manual** - サブスクライバーを更新するには、手動で ID 範囲を割り当てる必要があります。  
  
    -   **none** - パブリッシャーの ID 列は、サブスクライバーの ID 列として定義されません。  
  
     アーティクルの定義の詳細については、「[Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」 (アーティクルの定義) を参照してください。  
  
2.  サブスクライバーの更新時に競合が発生しないように、サブスクライバーの ID アーティクル列に範囲を割り当てます。  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションの既存のアーティクルに対する ID 範囲管理設定を自動的に変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md) を実行し、結果セットの **identityrangemanagementoption** の値を確認します。 値が **0**の場合、自動 ID 範囲管理は有効ではありません。  
  
2.  結果セットの **identityrangemanagementoption** の値が **1**の場合、次のようにして設定を変更します。  
  
    -   割り当てられている ID 範囲を変更するには、パブリッシャー側のパブリケーション データベースに対して [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) を実行します。 **\@property** に **identity_range** か **pub_identity_range** を指定し、 **\@value** に新しい範囲値を指定します。  
  
    -   新しい範囲の割り当てのしきい値を変更するには、パブリッシャー側のパブリケーション データベースに対して [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) を実行します。 **\@property** に **threshold** を指定し、 **\@value** に新しいしきい値を指定します。  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-merge-publication"></a>マージ パブリケーションの既存のアーティクルに対する ID 範囲管理設定を自動的に変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) を実行し、結果セットの **identity_support** の値を確認します。 値が **0**の場合、自動 ID 範囲管理は有効ではありません。  
  
2.  結果セットの **identity_support** の値が **1**の場合、次のようにして設定を変更します。  
  
    -   割り当てられている ID 範囲を変更するには、パブリッシャー側のパブリケーション データベースに対して [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。 **\@property** に **identity_range** か **pub_identity_range** を指定し、 **\@value** に新しい範囲値を指定します。  
  
    -   新しい範囲の割り当てのしきい値を変更するには、パブリッシャー側のパブリケーション データベースに対して [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。 **\@property** に **threshold** を指定し、 **\@value** に新しいしきい値を指定します。 いつ新しい ID 範囲が割り当てられるのかについては、「[ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)」の「ID 範囲の割り当て」を参照してください。  
  
    -   自動 ID 範囲管理を無効にするには、パブリッシャー側のパブリケーション データベースに対して [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。 **\@property** に **identityrangemanagementoption** を指定し、 **\@value** に **manual** または **none** を指定します。  
  
## <a name="see-also"></a>参照  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [ID 列のレプリケート](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
