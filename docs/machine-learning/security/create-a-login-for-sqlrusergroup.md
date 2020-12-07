---
title: SQLRUserGroup のログインｎ作成
description: ID を呼び出し元のユーザーに変換するために、暗黙の認証を使用して SQL Server 内で SQLRUserGroup 用のログインを作成してサーバーにログインします。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/25/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fcdb8353abe029291352f031d5261849514ef8fd
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/01/2020
ms.locfileid: "92195756"
---
# <a name="create-a-login-for-sqlrusergroup"></a>SQLRUserGroup のログインｎ作成
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

スクリプト内の [ループ バック接続](../../relational-databases/security/authentication-access/create-a-login.md)が [信頼関係接続](../concepts/security.md#sqlrusergroup)を指定するとき、 [SQLRUserGroup](../../machine-learning/concepts/security.md#implied-authentication) のための *SQL Server へのログイン* を作成すると、あなたのコードを含むオブジェクトの実行に使用される ID は Windows のユーザー アカウントです。

信頼関係接続とは、接続文字列に `Trusted_Connection=True` を持つ接続のことです。 SQL Server が信頼関係接続を指定する要求を受信すると、現在の Windows ユーザーの ID にログインがあるかどうかを確認します。 ワーカー アカウント ( **SQLRUserGroup** からの MSSQLSERVER01 など) として実行されている外部プロセスの場合、既定ではこれらのアカウントにはログインがないため、要求は失敗します。

**SQLServerRUserGroup** のログインを作成することによって、接続エラーを回避できます。 ID と外部プロセスの詳細については、「[機能拡張フレームワークのセキュリティの概要](../concepts/security.md)」を参照してください。

> [!Note]
> **SQLRUserGroup** に "ローカル ログオンを許可する" アクセス許可があることを確認します。 既定では、この権限はすべての新しいローカル ユーザーに与えられますが、グループ ポリシー付きの組織の一部では、この権限が無効になる場合があります。

## <a name="create-a-login"></a>ログインを作成します

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のオブジェクト エクスプローラーで、 **[セキュリティ]** を展開し、 **[ログイン]** を右クリックして、 **[新しいログイン]** を選択します。

2. **[ログイン - 新規作成]** ダイアログ ボックスで、 **[検索]** をクリックします。 (まだボックスに何も入力しないでください)。
    
     ![[検索] をクリックして機械学習用の新しいログインを追加する](media/implied-auth-login1.png "[検索] をクリックして機械学習用の新しいログインを追加する")

3. **[ユーザーまたはグループの選択]** ボックスで、 **[オブジェクトの種類]** ボタンをクリックします。

     ![[オブジェクトの種類] を検索して機械学習用の新しいログインを追加する](media/implied-auth-login2.png "[オブジェクトの種類] を検索して機械学習用の新しいログインを追加する")

4. **[オブジェクトの種類]** ダイアログ ボックスで、 **[グループ]** を選択します。 他のチェック ボックスはすべてオフにします。

     ![[オブジェクトの種類] ダイアログ ボックスでグループを選択する](media/implied-auth-login3.png "[オブジェクトの種類] ダイアログ ボックスでグループを選択する")

4. **[詳細]** をクリックして、検索する場所が現在のコンピューターであることを確認し、 **[検索開始]** をクリックします。

     ![[検索開始] をクリックしてグループの一覧を取得する](media/implied-auth-login4.png "[検索開始] をクリックしてグループの一覧を取得する")

5. サーバー上のグループ アカウントの一覧を、`SQLRUserGroup` で始まるものが見つかるまでスクロールします。
    
    + Launchpad サービスの _既定のインスタンス_ に関連付けられているグループの名前は、R または Python もしくはその両方のどれをインストールしたかにかかわらず、常に **SQLRUserGroup** です。 既定のインスタンスに対してのみ、このアカウントを選択します。
    + _名前付きインスタンス_ を使用している場合、インスタンス名は、既定のワーカー グループ名である `SQLRUserGroup` に追加されます。 たとえば、インスタンスの名前が "MLTEST" の場合、このインスタンスの既定のユーザー グループ名は **SQLRUserGroupMLTest** となります。
 
    ![サーバー上のグループ例](media/implied-auth-login5.png "サーバー上のグループ例")
   
5. **[OK]** をクリックして [詳細設定] ダイアログ ボックスを閉じます。

    > [!IMPORTANT]
    > インスタンスに適切なアカウントを選択していることを確認してください。 各インスタンスは、独自の Launchpad サービスと、そのサービス用に作成されたグループのみを使用できます。 インスタンスは、Launchpad サービスまたはワーカー アカウントを共有できません。

6. **[OK]** をもう一度クリックして、 **[ユーザーまたはグループの選択]** ダイアログ ボックスを閉じます。

7. **[ログイン - 新規作成]** ダイアログ ボックスで、 **[OK]** をクリックします。 既定では、ログインは **Public** ロールに割り当てられ、データベース エンジンに接続するためのアクセス許可を与えられます。

## <a name="next-steps"></a>次のステップ

+ [セキュリティの概要](../concepts/security.md)
+ [機能拡張フレームワーク](../concepts/extensibility-framework.md)