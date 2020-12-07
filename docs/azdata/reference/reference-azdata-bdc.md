---
title: azdata bdc リファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cc10491dc6fbdd09f543260ccd4ef751cb9a21d1
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358310"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark コマンドを使用してセッション、ステートメント、およびバッチを作成および管理することで、ユーザーは Spark システムと対話できます。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS モジュールには、HDFS ファイル システムにアクセスするコマンドが用意されています。
[azdata bdc create](#azdata-bdc-create) | ビッグ データ クラスターを作成します。
[azdata bdc delete](#azdata-bdc-delete) | ビッグ データ クラスターを削除します。
[azdata bdc upgrade](#azdata-bdc-upgrade) | SQL Server ビッグ データ クラスターの各コンテナーにデプロイされているイメージを更新します。
[azdata bdc config](reference-azdata-bdc-config.md) | 構成コマンド。
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | エンドポイント コマンド。
[azdata bdc debug](reference-azdata-bdc-debug.md) | デバッグ コマンド。
[azdata bdc status](reference-azdata-bdc-status.md) | BDC の状態コマンド。
[azdata bdc control](reference-azdata-bdc-control.md) | 制御サービス コマンド。
[azdata bdc sql](reference-azdata-bdc-sql.md) | SQL サービス コマンド。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS サービス コマンド。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark サービス コマンド。
[azdata bdc gateway](reference-azdata-bdc-gateway.md) | ゲートウェイ サービス コマンド。
[azdata bdc app](reference-azdata-bdc-app.md) | アプリ サービス コマンド。
## <a name="azdata-bdc-create"></a>azdata bdc create
SQL Server ビッグ データ クラスターを作成します。Kubernetes の構成と環境変数 ['AZDATA_USERNAME', 'AZDATA_PASSWORD'] がシステムに必要です。
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  
[--accept-eula -a]  
                  
[--node-label -l]  
                  
[--force -f]
```
### <a name="examples"></a>例
ガイド付きの BDC 展開のエクスペリエンス。必要な値の入力を求めるプロンプトが表示されます。
```bash
azdata bdc create
```
引数と、`azdata bdc config init` を介して初期化されたカスタム構成プロファイルを使用した BDC 展開。
```bash
azdata bdc create --accept-eula yes --config-profile ./path/to/config/profile
```
カスタム クラスター名が指定され、既定の構成プロファイルが aks-dev-test である BDC 展開。
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test
```
引数を使用した BDC 展開。--force フラグが使用されるため、プロンプトは表示されません。
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--name -n`
ビッグ データ クラスターの名前。kubernetes 名前空間に使用されます。
#### `--config-profile -c`
クラスターの展開に使用されるビッグ データ クラスター構成プロファイル: ['openshift-prod', 'aks-dev-test-ha', 'aro-dev-test-ha', 'aks-dev-test', 'kubeadm-prod', 'aro-dev-test', 'openshift-dev-test', 'kubeadm-dev-test']
#### `--accept-eula -a`
Do you accept the license terms? (ライセンス条項に同意しますか?) [yes/no]. ([はい/いいえ]。) この引数を使用しない場合は、環境変数 ACCEPT_EULA を 'yes' に設定できます。 azdata のライセンス条項については、 https://aka.ms/eula-azdata-en を参照してください。
#### `--node-label -l`
ビッグ データ クラスター ノードのラベル。展開先のノードを指定するために使用されます。
#### `--force -f`
強制的に作成すると、ユーザーは値の入力を求められず、すべての問題が stderr の一部として出力されます。
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。
## <a name="azdata-bdc-delete"></a>azdata bdc delete
SQL Server ビッグ データ クラスターを削除します。Kubernetes の構成がシステムに必要です。
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>例
BDC の削除。
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
ビッグ データ クラスターの名前。kubernetes 名前空間に使用されます。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--force -f`
ビッグ データ クラスターを強制的に削除します。
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。
## <a name="azdata-bdc-upgrade"></a>azdata bdc upgrade
SQL Server ビッグ データ クラスターの各コンテナーにデプロイされているイメージを更新します。 更新されるイメージは、渡した Docker イメージに基づきます。 更新されるイメージが、現在展開されているイメージとは別の Docker イメージ リポジトリからのものである場合は、"repository" パラメーターも必要です。
```bash
azdata bdc upgrade --name -n 
                   --tag -t  
                   
[--repository -r]  
                   
[--controller-timeout -k]  
                   
[--stability-threshold -s]  
                   
[--component-timeout -p]
```
### <a name="examples"></a>例
同じリポジトリからの新しいイメージ タグ "cu2" への BDC のアップグレード。
```bash
azdata bdc upgrade -t cu2
```
新しいリポジトリ "foo/bar/baz" からのタグ "cu2" を持つ新しいイメージへの BDC のアップグレード。
```bash
azdata bdc upgrade -t cu2 -r foo/bar/baz
```
同じリポジトリからのタグ "cu2" を持つ新しいイメージへの BDC のアップグレード。アップグレードは、コントローラーがアップグレードされるまで 30 分間、コントローラー db がアップグレードされるまで 30 分間待機します。 その後、残りのクラスターのアップグレードをクラッシュさせることなく、コントローラーとコントローラー db が実行されるのを 3 分間待機します。 アップグレードの後続の各フェーズは、完了するまでに 40 分かかります。
```bash
azdata bdc upgrade -t cu2 --controller-timeout=30 --component-timeout=40 --stability-threshold=3
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
ビッグ データ クラスターの名前。kubernetes 名前空間に使用されます。
#### `--tag -t`
クラスター内のすべてのコンテナーをアップグレードするターゲットの Docker イメージ タグ。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--repository -r`
クラスター内のすべてのコンテナーでイメージをプルする Docker リポジトリ。
#### `--controller-timeout -k`
アップグレードがロールバックされるまでの、コントローラーまたはコントローラー データベースのアップグレードを待機する分数。
#### `--stability-threshold -s`
アップグレード後、安定とマークされるまで待機する分数。
#### `--component-timeout -p`
(コントローラーのアップグレード後に) アップグレードを一時停止する前にアップグレードの各フェーズが完了するまで待機する分数。
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。

## <a name="next-steps"></a>次のステップ

他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。 

**azdata** ツールをインストールする方法の詳細については、「[azdata のインストール](..\install\deploy-install-azdata.md)」を参照してください。

