---
title: SQL Server Integration Services Scale Out の証明書を管理する | Microsoft Docs
description: この記事では、SSIS Scale Out Master と Scale Out Worker 間の通信をセキュリティで保護するために証明書を管理する方法について説明します。
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.custom: performance
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 0577e6f0e0d1bd78b71b2945977c313ff6a36afc
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100347434"
---
# <a name="manage-certificates-for-sql-server-integration-services-scale-out"></a>SQL Server Integration Services Scale Out の証明書を管理する

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



Scale Out Master と Scale Out Worker の間の通信を守るために、SSIS Scale Out では 2 つの証明書が使用されます。マスターに 1 つ、ワーカーに 1 つです。 

## <a name="scale-out-master-certificate"></a>Scale Out Master 証明書

ほとんどの場合、Scale Out Master 証明書は、Scale Out Master のインストール時に構成されます。

SQL Server インストール ウィザードの **[Integration Services Scale Out の構成 - マスター ノード]** ページで、新しい自己署名 TLS/SSL 証明書を作成するか、既存の TLS/SSL 証明書を使用するかを選択できます。

![マスターの構成](media/master-config.PNG)

**新しい証明書**。 証明書に対して特別な要件がない場合は、新しい自己署名 TLS/SSL 証明書の作成を選択できます。 さらに、証明書で CN を指定できます。 後で Scale Out Worker によって使用されるマスター エンドポイントのホスト名が CN に含まれていることを確認してください。 既定では、マスター ノードの IP アドレスとコンピューターの名前が含まれます。 

**既存の証明書**。 既存の証明書を使用することを選択する場合は、 **[参照]** をクリックし、ローカル コンピューターの **ルート** 証明書ストアから TLS/SSL 証明書を選択します。

### <a name="change-the-scale-out-master-certificate"></a>Scale Out Master 証明書の変更

証明書の有効期限などの理由により、Scale Out Master 証明書を変更する場合があります。 Scale Out Master 証明書を変更するには、次の作業を行います。

#### <a name="1-create-a-tlsssl-certificate"></a>1.TLS/SSL 証明書を作成する
次のコマンドを使用して、新しい TLS/SSL 証明書を作成し、マスター ノードにインストールします。

```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine -a sha1
```
次に例を示します。

```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine -a sha1
```

#### <a name="2-bind-the-certificate-to-the-master-port"></a>2.証明書をマスター ポートにバインドする
次のコマンドを使用して、元のバインドを確認します。

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

次に例を示します。

```dos
netsh http show sslcert ipport=0.0.0.0:8391
```

次のコマンドを使用して、元のバインドを削除し、新しいバインドを設定します。

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={TLS/SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```

次に例を示します。

```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```

#### <a name="3-update-the-scale-out-master-service-configuration-file"></a>3.Scale Out Master サービス構成ファイルを更新する
マスター ノードで Scale Out Master サービス構成ファイル `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config` を更新します。 **SSLCertThumbprint** を新しい TLS/SSL 証明書のサムプリントに更新します。

#### <a name="4-restart-the-scale-out-master-service"></a>4.Scale Out Master サービスを再起動する

#### <a name="5-reconnect-scale-out-workers-to-scale-out-master"></a>5.Scale Out Worker を Scale Out Master に再接続する
各 Scale Out Worker に対し、Worker を削除して [Scale Out Manager](integration-services-ssis-scale-out-manager.md) を使用して再度追加するか、次の作業を行います。

a.  ワーカー ノードのローカル コンピューターのルート ストアにクライアント TLS/SSL 証明書をインストールします。

b.  Scale Out Worker サービス構成ファイルを更新します。

ワーカー ノードで Scale Out Worker サービス構成ファイル `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config` を更新します。 **MasterHttpsCertThumbprint** を新しい TLS/SSL 証明書のサムプリントに更新します。

c.  Scale Out Worker サービスを再起動します。

## <a name="scale-out-worker-certificate"></a>Scale Out Worker 証明書

Scale Out Worker 証明書は、Scale Out Worker のインストール時に自動的に生成されます。 

### <a name="change-the-scale-out-worker-certificate"></a>Scale Out Worker 証明書の変更

Scale Out Worker 証明書を変更する場合、次の作業を行います。

#### <a name="1-create-a-certificate"></a>1.証明書を作成する
次のコマンドを使用して、証明書を作成してインストールします。

```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

次に例を示します。

```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

#### <a name="2-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-worker-node"></a>2.ワーカー ノードのローカル コンピューターのルート ストアにクライアント証明書をインストールする

#### <a name="3-grant-service-access-to-the-certificate"></a>3.証明書にサービスのアクセス権を付与する
次のコマンドを使用して、古い証明書を削除して、新しい証明書に Scale Out Worker サービスのアクセス権を付与します。

```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```

次に例を示します。

```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```

#### <a name="4-update-the-scale-out-worker-service-configuration-file"></a>4.Scale Out Worker サービス構成ファイルを更新する
ワーカー ノードで Scale Out Worker サービス構成ファイル `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config` を更新します。 **WorkerHttpsCertThumbprint** を新しい証明書のサムプリントに更新します。

#### <a name="5-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-master-node"></a>5.マスター ノードのローカル コンピューターのルート ストアにクライアント証明書をインストールする

#### <a name="6-restart-the-scale-out-worker-service"></a>6.Scale Out Worker サービスを再起動する

## <a name="next-steps"></a>次のステップ
詳細については、次の記事を参照してください。
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
