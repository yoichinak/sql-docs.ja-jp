---
title: azdata bdc hdfs リファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc hdfs コマンドの参照記事。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b4f0795e6b1669a422a6d13826aa4a2cc447f2d8
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358530"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | HDFS シェルは、HDFS ファイル システムのための単純な対話型のコマンド シェルです。
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | 指定されたファイルまたはディレクトリの状態を一覧表示します。
[azdata bdc hdfs exists](#azdata-bdc-hdfs-exists) | ファイルまたはディレクトリが存在するかどうかを判定します。  存在する場合は True を、それ以外の場合は False を返します。
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | 指定されたパスにディレクトリを作成します。
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | 指定されたファイルまたはパスを指定された場所に移動します。
[azdata bdc hdfs create](#azdata-bdc-hdfs-create) | 指定された場所にテキスト ファイルを作成します。  単純なテキスト コンテンツは、データ パラメーターを使用して追加できます。
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | ファイルの内容を読み取ります。  オフセットと長さ (バイト単位) は省略可能なパラメーターです。
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | ファイルまたはディレクトリを削除します。
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | ファイルまたはディレクトリを再帰的に削除します。
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | 指定されたファイルまたはディレクトリに関するアクセス許可を変更します。
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | 指定されたファイルの所有者またはグループを変更します。
[azdata bdc hdfs cp](#azdata-bdc-hdfs-cp) | ローカル コンピューターと HDFS の間でファイルまたはディレクトリをコピーします。
[azdata bdc hdfs mount](reference-azdata-bdc-hdfs-mount.md) | HDFS 内のリモート ストアのマウントを管理します。
[azdata bdc hdfs status](reference-azdata-bdc-hdfs-status.md) | HDFS サービスの状態コマンド。
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
HDFS シェルは、HDFS ファイル システムのための単純な対話型のコマンド シェルです。
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>例
シェルを起動します。
```bash
azdata bdc hdfs shell
```
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
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
指定されたファイルまたはディレクトリの状態を一覧表示します。
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>例
状態を一覧表示します。
```bash
azdata bdc hdfs ls --path "tmp/"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
状態を一覧表示するパス。
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
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs exists
ファイルまたはディレクトリが存在するかどうかを判定します。  存在する場合は True を、それ以外の場合は False を返します。
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>例
ファイルまたはディレクトリの存在を確認します。
```bash
azdata bdc hdfs exists --path "tmp/"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
存在を確認するパス。
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
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
指定されたパスにディレクトリを作成します。
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>例
ディレクトリを作成します。
```bash
azdata bdc hdfs mkdir --path "tmp/"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
作成するディレクトリの名前。
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
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
指定されたファイルまたはパスを指定された場所に移動します。
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>例
ファイルまたはディレクトリを移動します。
```bash
azdata bdc hdfs mv --source-path "tmp/" --target-path "dest/"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--source-path -s`
移動するディレクトリ。
#### `--target-path -t`
移動先の場所。
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
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs create
指定された場所にテキスト ファイルを作成します。  単純なテキスト コンテンツは、データ パラメーターを使用して追加できます。
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>例
ファイルを作成します。
```bash
azdata bdc hdfs create --path "tmp/test.txt" --data "This is a test."
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
作成するファイルの名前。
#### `--data -d`
ファイルの内容。  単純なテキスト コンテンツを対象としています。
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
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
ファイルの内容を読み取ります。  オフセットと長さ (バイト単位) は省略可能なパラメーターです。
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    
--length -l
```
### <a name="examples"></a>例
ファイルを読み取ります。
```bash
azdata bdc hdfs cat --path "tmp/test.txt"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
読み取るファイルの名前。
#### `--offset`
読み取るファイル内のオフセットのバイト数。
#### `--length -l`
読み取るデータの長さ。
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
## <a name="azdata-bdc-hdfs-rm"></a>azdata bdc hdfs rm
ファイルまたはディレクトリを削除します。
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>例
ファイルまたはディレクトリを削除します。
```bash
azdata bdc hdfs rm --path "tmp/"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
削除するファイルの名前。
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
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
ファイルまたはディレクトリを再帰的に削除します。
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>例
ディレクトリを再帰的に削除します。
```bash
azdata bdc hdfs rmr --path "tmp/"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
再帰的に削除するファイルの名前。
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
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
指定されたファイルまたはディレクトリに関するアクセス許可を変更します。
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>例
ファイルまたはディレクトリのアクセス許可を変更します。
```bash
azdata bdc hdfs chmod --permission 775 --path "tmp/test.txt"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
アクセス許可を設定するファイルまたはディレクトリの名前。
#### `--permission`
設定するアクセス許可のオクテット。  例: "775"。
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
## <a name="azdata-bdc-hdfs-chown"></a>azdata bdc hdfs chown
指定されたファイルの所有者またはグループを変更します。
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      
--group -g
```
### <a name="examples"></a>例
所有者とグループを変更します。
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path "tmp/test.txt"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
所有者を変更するファイルまたはディレクトリの名前。
#### `--owner`
設定する所有者名。
#### `--group -g`
設定するグループ名。
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
## <a name="azdata-bdc-hdfs-cp"></a>azdata bdc hdfs cp
ローカル コンピューターと HDFS の間でファイルまたはディレクトリをコピーします。  入力がディレクトリの場合は、ディレクトリ ツリー全体がコピーされます。  ターゲット ファイルまたはディレクトリが存在する場合、コマンドは失敗します。  リモート HDFS ディレクトリを指定するには、パスにプレフィックス "hdfs:" を付けます
```bash
azdata bdc hdfs cp --from-path -f 
                   --to-path -t
```
### <a name="examples"></a>例
ローカル コンピューターと HDFS の間でファイルまたはディレクトリをコピーします。
```bash
azdata bdc hdfs cp --from_path "tmp/test.txt" --to-path "hdfs:/user/me/test.txt"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--from-path -f`
コピー元のパスの名前。  HDFS パスを示すには、パスにプレフィックス "hdfs:" を付けます。
#### `--to-path -t`
コピー先のパスの名前。  HDFS パスを示すには、パスにプレフィックス "hdfs:" を付けます。
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

