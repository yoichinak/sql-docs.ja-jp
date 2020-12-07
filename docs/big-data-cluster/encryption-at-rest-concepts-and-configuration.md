---
title: 保存時の暗号化
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスターでの保存時の暗号化についてすべて説明します。
author: dacoelho
ms.author: dacoelho
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/19/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: de0bc20d7551e8d42c5dc1463fada6ffcbb6a0fd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257152"
---
# <a name="encryption-at-rest-concepts-and-configuration-guide"></a>保存時の暗号化の概念と構成ガイド

SQL Server ビッグ データ クラスター CU8 からは、保存時の包括的な暗号化機能セットを使用して、プラットフォームに格納されるすべてのデータにアプリケーション レベルの暗号化を提供できるようになります。 このガイドでは、SQL Server ビッグ データ クラスターに対する保存時の暗号化機能セットの概念、アーキテクチャ、構成について説明します。

SQL Server ビッグ データ クラスターのデータは、次の 2 つの場所に格納されます。

* __SQL Server__ マスター インスタンス
* 記憶域プールと Spark によって使用される __HDFS__ 。

SQL Server ビッグ データ クラスターのデータを透過的に暗号化できるようにするには、次の 2 つの方法が考えられます。

* __ボリューム暗号化__ 。 このアプローチは、Kubernetes プラットフォームによってサポートされており、ビッグ データ クラスターの展開に対するベスト プラクティスと考えられます。 このガイドでは、ボリューム暗号化については説明しません。 SQL Server ビッグ データ クラスターに使用されるボリュームを適切に暗号化する方法については、Kubernetes プラットフォームまたはアプライアンスのドキュメントを参照してください。
* __アプリケーション レベルの暗号化__ 。 このアーキテクチャは、ディスクに書き込まれる前のデータを処理するアプリケーションによるデータの暗号化を指します。 ボリュームが公開されている場合、攻撃者は、復元先のシステムも同じ暗号化キーで構成されていない限り、データ成果物を他の場所に復元することはできません。 

SQL Server および HDFS コンポーネントのアプリケーション レベルの暗号化の主要なシナリオは、SQL Server ビッグ データ クラスターの保存時暗号化機能セットによってサポートされています。

次の機能が提供されています。

* __保存時のシステム管理の暗号化__ 。 この機能は、CU8 で使用できます。
* __保存時のユーザー管理の暗号化 (BYOK)__ 。サービス管理と外部キー プロバイダー統合の両方。 現在、サービス管理のユーザー作成キーのみがサポートされています。

## <a name="key-definitions"></a>重要な定義

### <a name="sql-server-big-data-clusters-key-management-service-kms"></a>SQL Server ビッグ データ クラスター キー管理サービス (KMS)

SQL Server BDC クラスターに対する保存時暗号化機能セット用のキーと証明書の管理を担当する、コントローラーでホストされたサービス。 次の機能をサポートするサービスです。

* 保存時の暗号化に使用されるキーと証明書のセキュリティで保護された管理と格納。
* Hadoop KMS の互換性。 BDC 上の HDFS コンポーネントのキー管理サービスとして機能します。
* SQL Server の TDE 証明書の管理。

現時点では、次の機能はサポートされていません。
* " *キーのバージョン管理のサポート* "。 

このドキュメントの残りの部分では、このサービスを __BDC KMS__ と呼びます。 また、 __BDC__ という用語は、 __SQL Server ビッグ データ クラスター__ コンピューティング プラットフォームに対しても使用します。

### <a name="system-managed-keys-and-certificates"></a>システム管理のキーと証明書

BDC KMS サービスにより、SQL Server と HDFS のすべてのキーと証明書が管理されます。

### <a name="user-provided-certificates"></a>ユーザー指定の証明書

BDC KMS によって管理されるユーザー指定のキーと証明書。一般に、BYOK (Bring Your Own Key) と呼ばれます。

### <a name="external-providers"></a>外部プロバイダー

BDC KMS と互換性のある、外部委任用の外部キー ソリューション。 この機能は、現時点ではサポートされていません。

## <a name="encryption-at-rest-on-sql-server-big-data-clusters-cu8"></a>SQL Server ビッグ データ クラスター CU8 での保存時の暗号化

SQL Server ビッグ データ クラスター CU8 は、保存時の暗号化機能セットの最初のリリースです。 このドキュメントをよく読み、お客様のシナリオを完全に評価してください。

この機能セットにより、SQL Server と HDFS の両方での保存時のデータの暗号化に対してシステム管理のキーと証明書を提供するための、 __BDC KMS コントローラー サービス__ が導入されます。 それらのキーと証明書は、サービスによって管理されます。このドキュメントでは、サービスとやりとりする方法についての運用ガイダンスを提供します。

* __SQL Server__ のインスタンスは、確立された [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md) 機能を利用します。
* __HDFS__ は、各ポッド内のネイティブ Hadoop KMS を使用して、コントローラー上の BDC KMS とやりとりします。 これにより、HDFS 上のセキュリティで保護されたパスを提供する HDFS 暗号化ゾーンが有効になります。

### <a name="sql-server-instances"></a>SQL Server インスタンス

* システムによって生成された証明書は、SQL Server ポッドにインストールされ、TDE コマンドで使用されます。 システム管理の証明書の名前付け標準は `timestamp` + `TDECertificate` です。 たとえば、`TDECertificate2020_09_15_22_46_27` のようにします。
* マスター インスタンスの BDC でプロビジョニングされたデータベースとユーザー データベースは、自動的には暗号化されません。 DBA でインストールされている証明書を使用して、任意のデータベースを暗号化できます。
* コンピューティング プールと記憶域プールは、システム生成の証明書を使用して自動的に暗号化されます。
* データ プールの暗号化は、T-SQL の `EXECUTE AT` コマンドを使用すれば技術的には可能ですが、現時点では推奨されず、サポートされていません。 この手法を使用してデータ プール データベースを暗号化することは有効ではなく、必要な状態で暗号化が行われない可能性があります。 また、次のリリースに対する互換性のないアップグレード パスが作成されます。
* 現時点では、証明書のローテーションはありません。 HA のデプロイでない場合は、T-SQL のコマンドを使用して、暗号化を解除してから新しい証明書で暗号化することがサポートされています。
* 暗号化の監視は、既存の標準の TDE 用 SQL Server DMV で行われます。
* TDE が有効なデータベースのバックアップとクラスターへの復元がサポートされています。
* HA はサポートされています。 SQL Server のプライマリ インスタンス上のデータベースが暗号化されている場合、データベースのすべてのセカンダリ レプリカも暗号化されます。

### <a name="hdfs-encryption-zones"></a>HDFS 暗号化ゾーン

* HDFS に対して暗号化ゾーン機能を有効にするには、[Active Directory 統合](active-directory-prerequisites.md)が必要です。
* システム生成のキーは、Hadoop KMS でプロビジョニングされます。 キー名は `securelakekey` です。 CU8 での既定のキーは 256 ビットであり、256 ビットの AES 暗号化がサポートされています。
* 既定の暗号化ゾーンは、`/securelake` という名前のパス上にある上記のシステム生成キーを使用してプロビジョニングされます。
* ユーザーは、このガイドで説明されている具体的な手順を使用して、追加のキーと暗号化ゾーンを作成できます。 ユーザーは、キーを作成するときに、128、192、または 256 のキー サイズを選択できます。
* HDFS に対するインプレースのキー ローテーションは、CU8 では使用できません。 代わりの方法として、distcp を使用して、異なる暗号化ゾーン間でデータを移動できます。
* 暗号化ゾーンの上への HDFS 階層化マウントの実行はサポートされていません。

## <a name="configuration-guide"></a>構成ガイド

SQL Server ビッグ データ クラスターの保存時の暗号化はサービスで管理された機能であり、展開パスによっては、追加の手順が必要になる場合があります。

__SQL Server ビッグ データ クラスターを新しく展開する__ 間に、CU8 以降では、 __保存時の暗号化が既定で有効になって構成されます__ 。 これは次のことを意味します。

* コントローラーに展開される BDC KMS コンポーネントにより、キーと証明書の既定のセットが生成されます。
* SQL Server は TDE をオンにして展開され、コントローラーによって証明書がインストールされます。
* Hadoop KMS (HDFS の場合) は、暗号化操作のため BDC KMS とやりとりするように構成されます。 HDFS 暗号化ゾーンが構成され、使用できるようになります。

前のセクションで説明した要件と既定の動作が適用されます。

__クラスターを CU8 にアップグレードする__ 場合は、 __次のセクションをよくお読みください__ 。

### <a name="upgrading-to-cu8"></a>CU8 へのアップグレード

   > [!CAUTION]
   > SQL Server ビッグ データ クラスター CU8 にアップグレードする前に、データの完全バックアップを実行します。

既存クラスターのアップグレード プロセスにおいては、ユーザー データに対して暗号化は適用されず、HDFS 暗号化ゾーンは構成されません。 この動作は仕様であり、コンポーネントごとに以下のことを考慮する必要があります。

* __SQL Server__

    1. __SQL Server マスター インスタンス__ 。 アップグレード プロセスによって、マスター インスタンス データベースおよびインストールされている TDE 証明書は影響を受けませんが、アップグレード プロセスの前に、データベースと手動でインストールした TDE 証明書をバックアップすることを強くお勧めします。 また、それらの成果物を SQL Server BDC クラスターの外部に格納することもお勧めします。
    1. __コンピューティングと記憶域プール__ 。 それらのデータベースは、システムで管理され、揮発性であり、クラスターのアップグレード時に再作成されて自動的に暗号化されます。
    1. __データ プール__ 。 データ プールの SQL Server インスタンス部分のデータベースには、アップグレードによる影響はありません。

* __HDFS__

    1. __HDFS__ 。 アップグレード プロセスにより、暗号化ゾーンの外部にある HDFS ファイルやフォルダーは処理されません。
    1. __暗号化ゾーンは構成されません__ 。 Hadoop KMS コンポーネントは、BDC KMS を使用するように構成されません。 アップグレード後に HDFS 暗号化ゾーン機能を構成して有効にするには、次のセクションのようにします。

### <a name="enable-hdfs-encryption-zones-after-upgrade"></a>アップグレード後に HDFS 暗号化ゾーンを有効にする

クラスターを CU8 (`azdata upgrade`) にアップグレードし、HDFS 暗号化ゾーンを有効にしたい場合は、次の操作を実行します。

要件:

- [Active Directory](active-directory-prerequisites.md) 統合クラスター。

- AD モードで構成され、クラスターにログインしている [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]。

暗号化ゾーンをサポートするようにクラスターを再構成するには、次の手順のようにします。

1. `azdata` でアップグレードを実行した後、次のスクリプトを保存します。

    スクリプトの実行要件:
        
    * 両方のスクリプトが同じディレクトリ内に存在する必要があります。 
    * `PATH 上の `kubectl`
    * フォルダー ```$HOME/.kube``` 内の Kubernetes 用の ```config``` ファイル
    
    このスクリプトは、 __```run-key-provider-patch.sh```__ という名前にする必要があります。

    ```console
    #!/bin/bash
    
    if [[ -z "${BDC_DOMAIN}" ]]; then
      echo "BDC_DOMAIN environment variable with the domain name of the cluster is not defined."
      exit 1
    fi
    
    if [[ -z "${BDC_CLUSTER_NS}" ]]; then
      echo "BDC_CLUSTER_NS environment variable with the cluster namespace is not defined."
      exit 1
    fi
    
    kubectl get configmaps -n test
    
    diff <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py) <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | python -m json.tool)
    
    diff <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py) <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | python -m json.tool)
    
    # Replace the config maps.
    #
    kubectl replace -n $BDC_CLUSTER_NS -o json -f <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py)
    
    kubectl replace -n $BDC_CLUSTER_NS -o json -f <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py)
    
    # Restart the pods which need to have the necessary changes with the core-site.xml
    kubectl delete pods -n $BDC_CLUSTER_NS nmnode-0-0
    kubectl delete pods -n $BDC_CLUSTER_NS storage-0-0
    kubectl delete pods -n $BDC_CLUSTER_NS storage-0-1
    
    # Wait for sometime for pods to restart
    #
    sleep 300
    
    # Check for the KMS process status.
    #
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop nmnode-0-0 -- bash -c 'ps aux | grep kms'
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop storage-0-0 -- bash -c 'ps aux | grep kms'
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop storage-0-1 -- bash -c 'ps aux | grep kms'
    ```

    このスクリプトは、 __```updatekeyprovider.py```__ という名前にする必要があります。

    ```python
    #!/usr/bin/env python3
    
    import json
    import re
    import sys
    import xml.etree.ElementTree as ET
    import os
    
    class CommentedTreeBuilder(ET.TreeBuilder):
        def comment(self, data):
            self.start(ET.Comment, {})
            self.data(data)
            self.end(ET.Comment)
    
    domain_name = os.environ['BDC_DOMAIN']
    
    parser = ET.XMLParser(target=CommentedTreeBuilder())
    
    core_site = 'core-site.xml'
    j = json.load(sys.stdin)
    cs = j['data'][core_site]
    csxml = ET.fromstring(cs, parser=parser)
    props = [prop.find('value').text for prop in csxml.findall(
        "./property/name/..[name='hadoop.security.key.provider.path']")]
    
    kms_provider_path=''
    
    for x in range(5):
        if len(kms_provider_path) != 0:
            kms_provider_path = kms_provider_path + ';'
        kms_provider_path = kms_provider_path + 'nmnode-0-0.' + domain_name
    
    if len(props) == 0:
        prop = ET.SubElement(csxml, 'property')
        name = ET.SubElement(prop, 'name')
        name.text = 'hadoop.security.key.provider.path'
        value = ET.SubElement(prop, 'value')
        value.text = 'kms://https@' + kms_provider_path + ':9600/kms'
        cs = ET.tostring(csxml, encoding='utf-8').decode('utf-8')
    
    j['data'][core_site] = cs
    
    kms_site = 'kms-site.xml.tmpl'
    ks = j['data'][kms_site]
    
    kp_uri_regex = re.compile('(<name>hadoop.kms.key.provider.uri</name>\s*<value>\s*)(.*)(\s*</value>)', re.MULTILINE)
    
    def replace_uri(match_obj):
        key_provider_uri = 'bdc://https@hdfsvault-svc.' + domain_name
        if match_obj.group(2) == 'jceks://file@/var/run/secrets/keystores/kms/kms.jceks' or match_obj.group(2) == key_provider_uri:
            return match_obj.group(1) + key_provider_uri + match_obj.group(3)
        return match_obj.group(0)
    
    ks = kp_uri_regex.sub(replace_uri, ks)
    
    j['data'][kms_site] = ks
    print(json.dumps(j, indent=4, sort_keys=True))
    ```

    適切なパラメーターを使用して __```run-key-provider-patch.sh```__ を実行します。 

## <a name="next-steps"></a>次のステップ

SQL Server ビッグ データ クラスターの保存時の暗号化を効果的に使用する方法の詳細については、次の記事を参照してください。

- [保存時の暗号化 - SQL Server TDE](encryption-at-rest-sql-server-tde.md)
- [保存時の暗号化 - HDFS 暗号化ゾーン](encryption-at-rest-hdfs-encryption-zones.md)

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、次の概要を参照してください。

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)
