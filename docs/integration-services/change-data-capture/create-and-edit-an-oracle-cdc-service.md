---
description: Oracle CDC Service の作成と編集
title: Oracle CDC Service の作成と編集 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 10cd612e-d8f1-4af2-97d3-a0c22e1e2326
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bcccb89d1af55f990388b389087c16c003d12c39
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130655"
---
# <a name="create-and-edit-an-oracle-cdc-service"></a>Oracle CDC Service の作成と編集

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  新しい Oracle CDC Windows Service の作成と編集は CDC Service 構成コンソールで行います。  
  
 新しい Oracle CDC Windows Service を作成するには、左側のペインで **[ローカルの CDC Service]** を選択し、 **[アクション]** ペインで **[新しいサービス]** をクリックします。 **[ローカルの CDC Service]** を右クリックして **[新しいサービス]** をクリックすることもできます。 [新しい Oracle CDC Windows Service] ダイアログ ボックスが表示されます。  
  
 **OR**  
  
 CDC Service のプロパティを編集するには、プロパティを編集するサービスを選択し、 **[アクション]** ペインの **[プロパティ]** をクリックします。 操作するサービスを右クリックし、 **[プロパティ]** をクリックすることもできます。 [CDC Service のプロパティ] ダイアログ ボックスが表示されます。  
  
 [新しい Oracle CDC Windows Service] ダイアログ ボックスまたは [CDC Service のプロパティ] ダイアログ ボックスに次の情報を入力します。  
  
**サービス名**  
 新しい Oracle CDC Windows Service の名前を入力します。 可能な限り長い名前は使用しないでください。 / 文字および \ 文字はサービス名で使用できません。  
  
> [!NOTE]  
> このオプションは、サービスを編集するときは使用できません。 既に存在する Windows サービスの名前を変更することはできません。  
  
 **説明**  
 サービスを識別するのに役立つ説明を入力します。  
  
 **[サービス アカウント]**  
 次のいずれかを選択して、サービスを実行するアカウントを決定します。  
  
-   **ローカル システム アカウント**  
  
     このオプションはサービスに与える権限が多すぎるため、お勧めしません。  
  
-   **[このアカウント]**  
  
     Windows Vista または Windows Server 2008 では、既定のサービス アカウントは NETWORK SERVICE アカウントです。  
  
     Windows 7 および Windows Server 2008 R2 以降では、既定のサービス アカウントは NT Service\\<service-name> です。  
  
     これらのアカウントにはパスワードが不要なため、これらのアカウントを使用すると、パスワードを使用せずに作業を行うことができます。 さらにこれらのアカウントは、Oracle CDC Service の実行に必要な権限のみを提供します。  
  
     ローカルまたはドメインの Windows アカウントをサービス アカウントに使用できます。 この場合、アカウントの **[パスワード]** を入力する必要があります。 このアカウントは、ローカル ホストまたはドメイン アカウント用にすることができます。 パスワードが変更されたときは、必ず Windows のコントロール パネルのローカル サービスを使用してパスワードを更新します。  
  
 **[サーバー名]** : 接続先となる対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを選択します (例: **\\\\<コンピューター名>\\<インスタンス名>** )。 既定では、最後に接続していたサーバー インスタンスが表示されます。  
  
 **認証**  
 次のいずれかを選択してください。  
  
-   **[Windows 認証]**: このオプションを選択した場合、Oracle CDC Service はサービス アカウント ID を使用して対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが異なるコンピューターで実行されている場合、Windows 認証をドメイン アカウントと共に使用する必要があります。  
  
-   **[SQL Server 認証]**: このオプションを選択する場合、使用する **ログインの** [ユーザー名] **と** [パスワード] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を入力する必要があります。 Oracle CDC Service は、対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続するときに、これらの資格情報を使用します。  
  
 Oracle CDC Service によって使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインは、public 固定サーバー ロールのメンバーであることだけが必要です。その他の権限は不要です。 新しい Oracle CDC インスタンスが追加されると、そのログインには、関連付けられている **CDC データベースへの** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクセスが与えられます。  
  
 Oracle CDC Windows Service の定義を作成するには、プログラムに、関連付けられている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内の MSXDBCDC データベースに対する更新アクセスが必要です。 **[OK]** をクリックすると、MSXDBCDC データベースに対する更新アクセスを持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを入力するためのダイアログ ボックスが表示されます。  
  
 [SQL Server への接続] ダイアログ ボックスに入力するデータについては、「 [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)」を参照してください。  
  
 **[オプション]**  
 矢印をクリックして、構成するオプションを表示します。 これらのオプションを既定値のままにすることもできます。 使用可能なオプションは次のとおりです。  
  
-   **[接続タイムアウト]** : CDC Service for Oracle が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続を待機する時間 (秒単位) を入力します。この時間を超過するとタイムアウトとなります。既定値は **15** です。  
  
-   **[実行タイムアウト]** : Oracle CDC Windows Service がコマンドの実行を待機する時間 (秒単位) を入力します。この時間を超過するとタイムアウトとなります。既定値は、 **30** です。  
  
-   **[暗号化接続]**: Oracle CDC Service とターゲットの **インスタンスの間の暗号化された接続を使用した通信に対しては、** [暗号化接続] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を選択します。  
  
-   **[詳細設定]**: 必要に応じて、追加の接続プロパティを入力します。  
  
 **[マスター パスワード]**  
 Oracle CDC Windows Service によって Oracle のログ マイニング資格情報を保護するために使用されるパスワードを入力します。  
  
 高可用性構成で同じサービスの他のインスタンスがクラスターの他のノードで構成されている場合、同じマスター パスワードを使用する必要があります。 マスター パスワードを紛失または変更した場合、Oracle CDC インスタンス データベースに格納されているすべてのログ マイニング パスワードを、CDC デザイナー コンソールを使用して再入力する必要があります。  
  
## <a name="see-also"></a>参照  
 [CDC Service を作成および編集する方法](../../integration-services/change-data-capture/how-to-create-and-edit-a-cdc-service.md)  
  
  
