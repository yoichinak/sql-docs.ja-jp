---
description: Oracle 接続マネージャー
title: Oracle 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 428ca450371e452081d548a64e26dba2bd29b3b5
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88430744"
---
# <a name="oracle-connection-manager"></a>Oracle 接続マネージャー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Oracle 接続マネージャーを使用して、Oracle データベースからのデータの抽出と Oracle データベースへのデータの読み込みを行うパッケージを有効にできます。

Oracle 接続マネージャーの **ConnectionManagerType** プロパティには、**ORACLE** が設定されます。

## <a name="configuring-the-oracle-connection-manager"></a>Oracle 接続マネージャーの構成

Oracle 接続マネージャーの構成の変更は、実行時に Integration Services によって解決されます。 **[Oracle 接続マネージャー]** ダイアログ ボックスを使用して、Oracle データ ソースへの接続を追加します。

![接続マネージャー](media/oracle-connection-manager.png)

### <a name="options"></a>オプション

#### <a name="connection-manager-information"></a>接続マネージャー情報

Oracle 接続に関する情報を入力します。

**名前**

Oracle 接続の名前を入力します。 既定の名前は、[Oracle 接続マネージャー] です。 

**説明** 

接続の説明を入力します。 この入力は省略可能です。

**TNS サービス名**

作業する Oracle データベースの名前を入力します。 次のような TNS サービス名を使用できます。

- Oracle クライアントの admin フォルダーに配置される tnsnames.ora ファイル内で定義されている接続記述子の名前。

- EzConnect 形式: [//]host[:port][/service_name]

詳細については Oracle のマニュアルを参照してください。

#### <a name="connection-manager-logging"></a>接続マネージャーのログ記録

次のいずれかのオプションを選択します。

- **Windows 認証を使用する**:Windows 認証を使用するには、これを選択します。

- **Oracle 認証を使用する**:Oracle データベース認証を使用するには、これを選択します。 この認証を使用する場合は、Oracle 資格情報を次のように入力します。  
    **ユーザー名**:Oracle データベースに接続するために使用するユーザー名を入力します。  
    **パスワード**:[ユーザー名] フィールドに入力したユーザーの Oracle データベース パスワードを入力します。

> [!NOTE]
>
>Oracle Server 18c では、Windows 認証はサポートされていません。

**[接続テスト]**

**[接続テスト]** をクリックして、指定した情報が正しいかどうかを確認します。 入力した情報で Oracle データベースに接続できる場合は、「**接続テストに成功しました**」というメッセージが表示されます。

### <a name="custom-properties"></a>カスタム プロパティ

Oracle 接続マネージャーには、次のカスタム接続マネージャー プロパティがあります。

- **EnableDetailedTracing**:使用されません。

- **OracleHome**:コネクタによって使用される 32 ビットの Oracle ホーム名またはフォルダーを指定します。 (省略可能)

- **OracleHome64**:64 ビット モードで実行する場合にコネクタによって使用される 64 ビットの Oracle ホーム名またはフォルダーを指定します。 (省略可能)

カスタム プロパティは、Oracle 接続マネージャー エディターには表示されません。 **OracleHome** プロパティと **OracleHome64** プロパティを設定するには:

1. [接続マネージャー] 領域で、作業中の Oracle 接続マネージャーを右クリックし、**[プロパティ]** を選択します。

2. **[プロパティ]** ウィンドウで、**OracleHome** プロパティまたは **OracleHome64** プロパティに Oracle ホーム ディレクトリへの完全なパスを設定します。

## <a name="next-steps"></a>次のステップ

- [Oracle ソース](oracle-source.md)を構成する。
- [Oracle 変換先](oracle-destination.md)を構成する。
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA5u35j)を参照してください。
