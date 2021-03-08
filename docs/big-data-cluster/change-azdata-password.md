---
title: AZDATA_PASSWORD を更新する
description: '`AZDATA_PASSWORD` を手動で更新する'
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 03/01/2021
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 062e574772c2a44b78772da4a979c81ed3deb959
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101836269"
---
# <a name="manually-update-azdata_password"></a>`AZDATA_PASSWORD` を手動で更新する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[!INCLUDE[ssbigdataclusters-ss-nover](../includes/ssbigdataclusters-ss-nover.md)]が Active Directory 統合で動作しているかどうかにかかわらず、展開時に `AZDATA_PASSWORD` が設定されます。 これにより、クラスター コントローラーとマスター インスタンスに基本認証が提供されます。 このドキュメントでは、`AZDATA_PASSWORD` を手動で更新する方法について説明します。

## <a name="change-azdata_password-for-controller"></a>コントローラーの `AZDATA_PASSWORD` を変更する

クラスターが非 Active Directory モードで動作している場合は、次の手順を実行して、Apache Knox ゲートウェイのパスワードを更新します。

1. 次のコマンドを実行して、コントローラーの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資格情報を取得します。

   a. Kubernetes 管理者として次のコマンドを実行します。

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. シークレットを Base64 でデコードします。
   
   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. 別のコマンド ウィンドウで、コントローラー データベースのサーバー ポートを公開します。

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```
 
1. 先ほど取得したシステム管理者パスワードを使用して、SQL クライアント ツールからコントローラー データベース サーバーに接続します。

1. `AZDATA_USERNAME` の新しい複雑なパスワードを生成して、既存の `AZDATA_PASSWORD` を置き換えます。

   生成されるパスワードは "newPassword" なので、この例を簡単にするために、次の手順では "newPassword" を使用します。 

1. users テーブルから `hexsalt` を取得します。

   ```sql
   SELECT hexsalt FROM [auth].[users] WHERE username = '<username>'
   ```

   `hexsalt` からランダムな 16 進文字列が返されます (たとえば、`64FC59DF31244FFEE02F457BC0750226`)。

1. `hexsalt` を使用して、新しい複雑なパスワードを暗号化します。

   参考までに、パスワードを暗号化するための事前に構築されたツール `pbkdf2` が用意されています。 [`pbkdf2`](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/security/password-hashing/pbkdf2/prebuilt-binaries) 用のプラットフォームに適した .NET Core アプリをダウンロードします。

   アプリは自己完結型であり、.NET ランタイムなどの必須コンポーネントは必要ありません。 パスワードを暗号化するには、以下を実行します。

   ```bash
   pbkdf2 <password> <hexsalt>
   J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=
   ```

1. users テーブルのパスワードを更新します。

   ```sql
   UPDATE [auth].[users] SET password = 'J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=' WHERE username = '<username>'
   ```

## <a name="change-azdata_password-in-the-sql-server-master-instance"></a>SQL Server マスター インスタンスの `AZDATA_PASSWORD` を変更する

1. 任意の管理者ユーザーを使用して、マスター SQL エンドポイントに接続します。

1. パラメーター `AZDATA_USERNAME` で展開時に定義したログイン資格情報のパスワードを変更するには、次の TSQL コマンドを実行します。

   ```sql
   ALTER LOGIN <AZDATA_USERNAME> WITH PASSWORD = 'newPassword'
   ```

## <a name="manually-updating-password-for-grafana-and-kibana"></a>Grafana と Kibana のパスワードを手動で更新する

手順に従って AZDATA_PASSWORD を更新した後も、[Grafana](app-monitor.md) と [Kibana](cluster-logging-kibana.md) で古いパスワードが引き続き受け付けられることがわかります。 これは、Grafana と Kibana からは Kubernetes の新しいシークレットを認識できないためです。 Grafana と Kibana のパスワードは、個別に手動で更新する必要があります。

## <a name="update-grafana-password"></a>Grafana のパスワードを更新する

[Grafana](app-monitor.md) のパスワードを手動で更新する場合は、次のオプションのようにします。

1. htpasswd ユーティリティが必要です。 これは任意のクライアント コンピューターにインストールできます。
    
    #### <a name="for-ubuntu"></a>[Ubuntu の場合](#tab/ubuntu): 
    ```bash
    sudo apt install apache2-utils
    ```
    
    #### <a name="for-rhel"></a>[RHEL の場合](#tab/rhel): 
    ```bash
    sudo yum install httpd-tools
    ```
    
    ---

2. 新しいパスワードを生成します。 
    
    ```bash
    htpasswd -nbs <username> <password>
    admin:{SHA}<secret>
    ```
    
    /<username/>、/<password/>、/<secret/> の値を、次の例のように適宜置き換えます。
    
    ```bash
    htpasswd -nbs admin Test@12345
    admin:{SHA}W/5VKRjIzjusUJ0ih0gHyEPjC/s=
    ```

3. 次に、パスワードをエンコードします。
    
    ```bash
    echo "admin:{SHA}W/5VKRjIzjusUJ0ih0gHyEPjC/s=" | base64
    ```             
    
    後のために、出力の base64 文字列を保持します。
    
4. 次に、mgmtproxy-secret を編集します。
    
    ```bash
    kubectl edit secret -n mssql-cluster mgmtproxy-secret
    ```
         
5. controller-login-htpasswd を、上で生成した新しいエンコードされたパスワードの base64 文字列で更新します。
    
    ```console
    # Please edit the object below. Lines beginning with a '#' will be ignored,
    # and an empty file will abort the edit. If an error occurs while saving this file will be
    # reopened with the relevant failures.
    #
    apiVersion: v1
    data:
       controller-login-htpasswd: <base64 string from before>
       mssql-internal-controller-password: <password>
       mssql-internal-controller-username: <username>
    ```         

6. mgmtproxy ポッドを見つけて削除します。 
     
    必要に応じて、mgmtproxy ポッドの名前を特定します。
    
    #### <a name="for-windows"></a>[Windows の場合](#tab/windows): 
    Windows サーバーでは、以下を使用できます。
    
    ```bash 
    kubectl get pods -n <namespace> -l app=mgmtproxy
    ```
    
    #### <a name="for-linux"></a>[Linux の場合](#tab/linux): 
    Linux では、以下を使用できます。
    
    ```bash
    kubectl get pods -n <namespace> | grep 'mgmtproxy'
    ```
    
    ---
    
    mgmtproxy ポッドを削除します。
    ```bash
    kubectl delete pod mgmtproxy-xxxxx -n mssql-clutser
    ```

7. mgmtproxy ポッドがオンラインになり、Grafana ダッシュボードが開始されるまで待ちます。  
 
    長く待つことはなく、ポッドは数秒以内にオンラインになるはずです。 ポッドの状態を確認するには、前のステップで使用したのと同じ `get pods` コマンドを使用できます。 
    mgmtproxy ポッドがすぐに準備完了状態に戻らない場合は、kubectl を使用してポッドを記述します。
    
    ```bash
    kubectl describe pods mgmtproxy-xxxxx  -n <namespace>
    ```
    
    トラブルシューティングを行ったり、さらにログを収集したりするには、Azure Data CLI の `[azdata bdc debug copy-logs](../azdata/reference/reference-azdata-bdc-debug.md)` コマンドを使用します。
    
8. 今度は、新しいパスワードを使用して Grafana にログインします。 


## <a name="update-the-kibana-password"></a>Kibana のパスワードを更新する

[Kibana](cluster-logging-kibana.md) のパスワードを手動で更新する場合は、次のオプションのようにします。

> [!NOTE]
> 古い Microsoft Edge ブラウザーには、Kibana との互換性がありません。ダッシュボードを正しく表示するには、Edge chromium ベースのブラウザーを使用する必要があります。 サポートされていないブラウザーを使用してダッシュボードを読み込むと、空のページが表示されます。[Kibana でサポートされているブラウザー](https://www.elastic.co/support/matrix#matrix_browsers)に関するページを参照してください。

1. Kibana の URL を開きます。
    
    Kibana のサービス エンドポイントの URL は、[Azure Data Studio](manage-with-controller-dashboard#controller-dashboard) 内から、または次の **azdata** コマンドを使用して、見つけることができます。
    
    ```azurecli
    azdata login
    azdata bdc endpoint list -e logsui -o table
    ```
    
    例: https://11.111.111.111:30777/kibana/app/kibana#/discover

2. 左側のペインで、 **[Security]\(セキュリティ\)** オプションをクリックします。
    
    ![セキュリティ オプションが選択されている、Kibana の左側のペインのメニューのスクリーンショット。](\media\big-data-cluster-change-kibana-password\big-data-cluster-change-kibana-password-1.jpg)

3. セキュリティ ページで、[Authentication Backends]\(認証バックエンド\) という見出しの下にある **[Internal User Database]\(内部ユーザー データベース\)** をクリックします。

    ![[Internal User Database]\(内部ユーザー データベース\) ボックスが選択されているセキュリティ ページのスクリーンショット。](\media\big-data-cluster-change-kibana-password\big-data-cluster-change-kibana-password-2.jpg)

4. これで、[Internal Users Database]\(内部ユーザー データベース\) という見出しの下にユーザーの一覧が表示されます。 このページを使用して、Kibana エンドポイント アクセスに関するユーザーの追加、変更、削除を行います。 更新されたパスワードを必要とするユーザーの場合は、ユーザーの右側にある **[Edit]\(編集\)** ボタンをクリックします。

    ![[Internal User Database]\(内部ユーザー データベース\) ページのスクリーンショット。 ユーザーの一覧で、KubeAdmin ユーザーの [Edit]\(編集\) ボタンが選択されています。](\media\big-data-cluster-change-kibana-password\big-data-cluster-change-kibana-password-3.jpg)

5. 新しいパスワードを 2 回入力し、 **[Submit]\(送信\)** をクリックします。

    ![内部ユーザー編集フォームのスクリーンショット。 [Password]\(パスワード\) フィールドと [Repeat password]\(パスワードの再入力\) フィールドに、新しいパスワードが入力されています。](\media\big-data-cluster-change-kibana-password\big-data-cluster-change-kibana-password-4.jpg)

6. ブラウザーを閉じ、更新されたパスワードを使用して Kibana の URL に再接続します。

> [!Note]
> 新しいパスワードを使用してログインした後、Kibana で空のページが表示される場合は、右上隅にあるログアウト オプションを使用して手動でログアウトし、もう一度ログインします。

## <a name="see-also"></a>関連項目

* [azdata bdc (Azure Data CLI)](../../sql/azdata/reference/reference-azdata-bdc.md) 
* [azdata と Grafana ダッシュボードでアプリケーションを監視する](app-monitor.md)  
* [Kibana ダッシュボードを使用してクラスター ログを確認する](cluster-logging-kibana.md)  