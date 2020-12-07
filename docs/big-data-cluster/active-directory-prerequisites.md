---
title: Active Directory モードでのデプロイ - 前提条件
titleSuffix: SQL Server Big Data Cluster
description: SQL Server ビッグ データ クラスターの Active Directory を構成する
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c25038680d71257e609d99460841d63b8e87d33
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91898713"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode-prerequisites"></a>Active Directory モードで [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] を展開する: 前提条件

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

このドキュメントでは、SQL Server ビッグ データ クラスター (BDC) の Active Directory 認証モードでのデプロイに向けて準備を行う方法について説明します。 クラスターでは、認証に既存の AD ドメインを使用します。

>[!Note]
>SQL Server 2019 CU5 リリースの前は、ビッグ データ クラスターに制限があるため、Active Directory ドメインに対してデプロイできるクラスターは 1 つだけでした。 この制限は、CU5 リリースで削除されています。新しい機能の詳細については、[概念: Active Directory モードで](active-directory-deployment-background.md) [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] をデプロイする方法に関するページを参照してください。 この記事の例は、デプロイの両方のユース ケースに対応するように調整されています。

## <a name="background"></a>バックグラウンド

Active Directory (AD) 認証を有効にするために、BDC では、クラスター内のさまざまなサービスで必要となるユーザー、グループ、コンピューター アカウント、サービス プリンシパル名 (SPN) が自動的に作成されます。 このようなアカウントを一部含め、スコーピングを許可するために、クラスター デプロイの前に組織単位 (OU) を作成することをお勧めします。 すべての BDC 関連の AD オブジェクトは、デプロイ中に作成されます。 

## <a name="pre-requisites"></a>前提条件

### <a name="organizational-unit-ou"></a>組織単位 (OU)
組織単位 (OU) は、ユーザー、グループ、およびその他の組織単位を配置する、Active Directory 内の区分です。 全体像としては、組織単位を使用して組織の機能やビジネスの構造を反映することができます。 この記事では、例として `bdc` という名前の OU を作成します。 

>[!NOTE]
>組織単位 (OU) は管理上の境界を表し、お客様がデータ管理者の権限の範囲を制御できるようになります。 

[OU の設計原則](/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts)に従って、組織内で OU を使用する際の最適な構造を決定することができます。

### <a name="ad-account-for-bdc-domain-service-account"></a>BDC ドメイン サービス アカウントの AD アカウント

BDC には、Active Directory で必要なすべてのオブジェクトを自動的に作成できるようにするために、指定した組織単位 (OU) 内にユーザー、グループ、およびコンピューター アカウントを作成するための特定のアクセス許可を持つ AD アカウントが必要です。 この記事では、この AD アカウントのアクセス許可を構成する方法について説明します。 この記事では、例として `bdcDSA` という AD アカウントを使用します。

### <a name="auto-generated-active-directory-objects"></a>自動的に生成される Active Directory のオブジェクト
BDC をデプロイすると、アカウントとグループ名が自動的に生成されます。 各アカウントは BDC 内の 1 つのサービスを表し、BDC クラスターが使用されている全有効期間にわたり BDC によって管理されます。 これらのアカウントにより、各サービスに必要なサービス プリンシパル名 (SPN) が所有されます。  AD の自動生成されるアカウント、グループ、およびそれらによって管理されるサービスの完全な一覧については、「[自動的に生成される Active Directory のオブジェクト](active-directory-objects.md)」をご覧ください。

>[!IMPORTANT]
>ドメイン コントローラーで設定されているパスワードの有効期限ポリシーによっては、これらのアカウントのパスワードの有効期限が切れることがあります。 既定の有効期限ポリシーは 42 日です。 BDC 内のすべてのアカウントの資格情報をローテーションするメカニズムはないため、有効期限が切れるとクラスターは動作しなくなります。 この問題を回避するには、ドメイン コントローラーで、BDC サービス アカウントの有効期限ポリシーを "パスワードを無期限にする" に更新します。 この操作は、有効期限の前または後に行うことができます。 後者の場合、Active Directory によって、期限切れのパスワードが再アクティブ化されます。
>
>次の図は、[Active Directory ユーザーとコンピューター] でこのプロパティを設定する場所を示しています。
>
>:::image type="content" source="media/deploy-active-directory/image25.png" alt-text="パスワードの有効期限のポリシーの設定":::

次の手順では、Active Directory ドメイン コントローラーを既に用意していることを前提としています。 ドメイン コントローラーがない場合、[こちら](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx)のガイドに含まれる手順が参考になります。

## <a name="create-ad-objects"></a>AD オブジェクトの作成

AD 統合で BDC を展開する前に次の操作を行います。

1. すべての BDC 関連の AD オブジェクトを格納する組織単位 (OU) を作成します。 または、デプロイ時に、既存の OU を選択することもできます。
1. BDC 用の AD アカウントを作成するか、既存のアカウントを使用し、この BDC の AD アカウントに指定した組織単位 (OU) の適切なアクセス許可を付与します。

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>BDC ドメイン サービス アカウントの AD でユーザーを作成する

ビッグ データ クラスターには、特定のアクセス許可を持つアカウントが必要です。 続行する前に、既存の AD アカウントを持っていることを確認するか、新しいアカウントを作成します。このアカウントは、ビッグ データ クラスターで必要なオブジェクトを設定するために使用できます。

AD で新しいユーザーを作成するには、ドメインまたは OU を右クリックし、 **[新規]** 、 **[ユーザー]** の順に選択します。

![Active Directory のユーザー ダイアログ](./media/deploy-active-directory/image12.png)

このユーザーは、この記事で *BDC ドメイン サービス アカウント*と呼びます。

### <a name="create-an-ou"></a>OU を作成する

ドメイン コントローラーで、 **[Active Directory ユーザーとコンピューター]** を開きます。 左側のパネルで、OU を作成するディレクトリを右クリックし、 **[新規]** \> **[組織単位]** の順に選択します。次に、ウィザードの指示に従って OU を作成します。 または、PowerShell で OU を作成できます。

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

この記事の例では、OU 名に `bdc` を使用しています。

![Active Directory 組織単位](./media/deploy-active-directory/image13.png)

![新しいオブジェクト - 組織単位](./media/deploy-active-directory/image14.png)

### <a name="set-permissions-for-an-ad-account"></a>AD アカウントのアクセス許可を設定する

新しい AD ユーザーを作成したか、既存の AD ユーザーを使用しているかに関係なく、ユーザーには特定のアクセス許可を与える必要があります。 このアカウントは、クラスターを AD に参加させるとき、BDC コントローラーによって使用されるユーザー アカウントです。

BDC ドメイン サービス アカウント (DSA) は、OU でユーザー、グループ、コンピューター アカウントを作成できる必要があります。 次の手順では、BDC ドメイン サービス アカウントに `bdcDSA` という名前を付けています。 このアカウントには任意の名前を選択できます。

1. ドメイン コントローラーで、 **[Active Directory ユーザーとコンピューター]** を開きます。

1. 左側のパネルでドメインに移動し、`bdc` で使用される OU に移動します。

1. OU を右クリックし、 **[プロパティ]** を選択します。

1. [セキュリティ] タブに移動します (OU を右クリックし、 **[表示]** を選択し、 **[高度な機能]** が選択されていることを確認してください)。

    ![BDC オブジェクトのプロパティ](./media/deploy-active-directory/image15.png)

1. **[追加]** をクリックし、**bdcDSA** ユーザーを追加します。

    ![BDC オブジェクトのプロパティを追加する](./media/deploy-active-directory/image16.png)

    ![オブジェクトを選択する](./media/deploy-active-directory/image17.png)

1. **bdcDSA** ユーザーを選択し、アクセス許可をすべて消去し、 **[詳細]** をクリックします。

1. **[追加]** をクリックします。

    ![[追加] をクリックする](./media/deploy-active-directory/image18.png)

    - **[プリンシパルの選択]** をクリックし、**bdcDSA** を挿入し、[OK] をクリックします。

    - **[種類]** を **[許可]** に設定します。

    - **[適用先]** を **[このオブジェクトとすべての子オブジェクト]** に設定します。

        ![プロパティを [許可] に設定する](./media/deploy-active-directory/image19.png)

    - 一番下までスクロールし、 **[すべて消去]** をクリックします。

    - スクロールで一番上まで戻り、次を選択します。
       - **すべてのプロパティの読み取り**
       - **すべてのプロパティの書き込み**
       - **コンピューター オブジェクトの作成**
       - **コンピューター オブジェクトの削除**
       - **グループ オブジェクトの作成**
       - **グループ オブジェクトの削除**
       - **ユーザー オブジェクトの作成**
       - **ユーザー オブジェクトの削除**

    - **[OK]**

- **[追加]** をクリックします。

    - **[プリンシパルの選択]** をクリックし、**bdcDSA** を挿入し、[OK] をクリックします。

    - **[種類]** を **[許可]** に設定します。

    - **[適用先]** を **[Descendant Computer objects]\(子コンピューター オブジェクト\)** に設定します。

    - 一番下までスクロールし、 **[すべて消去]** をクリックします。

    - スクロールで一番上まで戻り、 **[パスワードのリセット]** を選択します。

    - **[OK]**

- **[追加]** をクリックします。

    - **[プリンシパルの選択]** をクリックし、**bdcDSA** を挿入し、[OK] をクリックします。

    - **[種類]** を **[許可]** に設定します。

    - **[適用先]** を **[Descendant User objects]\(子ユーザー オブジェクト\)** に設定します。

    - 一番下までスクロールし、 **[すべて消去]** をクリックします。

    - スクロールで一番上まで戻り、 **[パスワードのリセット]** を選択します。

    - **[OK]**

- **[OK]** をさらに 2 回クリックしてダイアログ ボックスを開きます。

## <a name="next-steps"></a>次のステップ

[Active Directory モードで [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する](active-directory-deploy.md)

[SQL Server ビッグ データ クラスターの Active Directory 統合のトラブルシューティング](troubleshoot-active-directory.md)

[概念: Active Directory モードで [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] をデプロイする](active-directory-deployment-background.md)
