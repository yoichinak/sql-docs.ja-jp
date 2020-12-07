---
title: 手順 1:Ruby 用に開発環境を構成する
description: このファースト ステップ ガイドの手順 1 では、Ruby と ODBC Driver for SQL Server を開発環境にインストールします。
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6412015000a5f9dda09ea5d489c8080fd2e1c09
ms.sourcegitcommit: 2600a414c321cfd6dc6daf5b9bcbc9a99c049dc4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603363"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>手順 1:Ruby 開発用に開発環境を構成する
SQL Server 用の Ruby ドライバーを使用してアプリケーションを開発するには、前提条件を使用して開発環境を構成する必要があります。    
  
Ruby ドライバーでは TDS プロトコルが使用されます。これは SQL Server と Azure SQL Database で既定で有効になっています。  追加の構成は不要です。  
  
  
## <a name="windows"></a>Windows  
  
1.  **Ruby インストーラーをダウンロードします**。  
コンピューターに Ruby がインストールされていない場合は、インストールしてください。 初めて Ruby を使用する場合は、Ruby 2.2.X インストーラーを使用することをお勧めします。これにより、安定した言語と、互換性があり更新される幅広いパッケージ (gem) のリストが提供されます。 [Ruby ダウンロード ページ](https://rubyinstaller.org/downloads/)にアクセスし、適切な 2.1.x インストーラーをダウンロードします。 たとえば、64 ビットのコンピューターを使用している場合、Ruby 2.1.6 (x64) インストーラーをダウンロードします。   
  
2.  **Ruby をインストールします**。  
インストーラーをダウンロードしたら、次の操作を行います。  
a. ファイルをダブルクリックしてインストーラーを起動します。  
b. 言語を選択し、使用条件に同意します。  
c.  インストールの設定画面で、[Add Ruby executables to your PATH]\(Ruby の実行ファイルを PATH に追加する\) と [Associate `.rb` and `.rbw` files with this Ruby installation]\(拡張子 .rb と .rbw を Ruby の実行ファイルに関連付ける\) の両方の横にあるチェック ボックスをオンにします。  
  
3.  **Ruby DevKit をダウンロードします**。  
RubyInstaller ページから DevKit をダウンロードします。  
  
4.  **Ruby DevKit をインストールします**。  
ダウンロードが完了したら、次の操作を行います。  
a. ファイルをダブルクリックします。 ファイルの抽出先を確認するメッセージが表示されます。  
b. [...] ボタンをクリックし、[C:\DevKit] を選択します。 このフォルダーは、[新しいフォルダーの作成] をクリックして最初に作成する必要のある場合があります。  
c. [OK] をクリックし、[抽出] をクリックしてファイルを抽出します。  
  
5. **Cmd.exe を開きます**  
  
6. **Ruby DevKit を初期化します**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **TinyTDS gem をインストールします**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **ターミナルを開きます**  
  
2. **Ruby バージョン マネージャー (`rvm`) と前提条件をインストールします**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **`rvm` を使用して Ruby をインストールします**  
たとえば、Ruby バージョン 2.3.0 をインストールします。  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最後のコマンドの出力が、バージョン 2.3.0 が実行されていることを確実に示すようにします。  
  
4.  **FreeTDS をインストールします**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **TinyTDS をインストールします**  
```  
> gem install tiny_tds  
```  
  
## <a name="macos"></a>macOS  
  
注: macOS には、OS に依存関係があるため、既に Ruby がプレインストールされています。
  
1.  **ターミナルを開きます**  
  
2. **Homebrew パッケージ マネージャーをインストールします**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **FreeTDS をインストールします**  
```  
> brew install FreeTDS  
```  
  
4.  **TinyTDS gem をインストールします**  
```  
> gem install tiny_tds  
```
