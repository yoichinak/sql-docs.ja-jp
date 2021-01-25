---
title: SQL Server オプション ページ - Azure サービス
description: オプション (Azure サービス)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Azure_Services.Azure_Cloud
dev_langs:
- TSQL
author: markingmyname
ms.author: maghan
ms.date: 01/15/2021
ms.openlocfilehash: 0983317d1d5c59e486764532708c566bb740000a
ms.sourcegitcommit: 23649428528346930d7d5b8be7da3dcf1a2b3190
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "98245705"
---
# <a name="options-azure-services"></a>オプション (Azure サービス)

Azure クラウド サービスに関連するオプションを指定するには、このページを使用します。 このダイアログ ボックスにアクセスするには、上部のメニュー バーから **[ツール] > [オプション] [Azure サービス]** の順に選択します。

## <a name="miscellaneous"></a>その他

| オプション | 情報 | 説明 |
|--------|-------------|-------------|
| ADAL 出力ウィンドウ トレース レベル | **[情報]** <br> **なし** <br> **詳細** <br> **警告** | 出力ウィンドウに送信する Azure Active Directory (AAD) ログイン トレースのレベル。 |
| Azure Data Factory ポータルの URL | `https://adf.azure.com` | Azure Data Factory ポータルの URL を指定します。 |
| Azure SQL Database への条件付きアクセスを有効にする (試験段階) | **True** <br> **False** | 試験段階:true の場合、選択したサーバーへのアクセスの要求を含む Azure SQL Database のアクセス トークンを要求します。 設定を有効にするには、SSMS の再起動が必要になることがあります。 |
| ギャラリー エンドポイント | `https://gallery.azure.com` | デプロイ テンプレートの Resource Manager ギャラリーのエンドポイントを指定します。 |
| Graph の対象ユーザー | `https://graph.windows.net` | Graph エンドポイントのリソース ID。 |
| Graph エンドポイント | `https://graph.windows.net` | Azure Active Directory Graph 要求の URL を指定します。 |
| 管理ポータルの URL | `https://portal.azure.com` | 管理ポータルの URL を指定します。 |
| 発行設定ファイルの URL | `https://go.microsoft.com/fwlink/?LinkID=335839` | `.publishsettings` ファイルをダウンロードできる URL を指定します。 |
| SQL Database サービス プリンシパル名 | `https://database.windows.net/` | AAD 認証を使用するときにトークンを取得するための Azure SQL Database SPN。 また、サーバー側 JSON Web Token (JWT) 解析または検証のための JSON Web Token (JWT) の対象ユーザー。 |

## <a name="resource-management"></a>リソース管理

| オプション | 情報 | 説明 |
|--------|-------------|-------------|
| Active Directory オーソリティ | `https://login.microsoftonline.com` | Azure Active Directory (AAD) 認証用の基本オーソリティを指定します。 |
| Active Directory サービス エンドポイント リソース ID | `https://management.core.windows.net` | Azure Resource Manager (ARM) またはサービス管理 (RDFE) エンドポイントへの要求を認証するトークンの対象ユーザーを指定します。 |
| Resource Manager エンドポイント | `https://management.azure.com` | リソース管理要求の URL を指定します。 |
| サービス エンドポイント | `https://management.core.windows.net` | サービス管理要求のエンドポイントを指定します。 |

## <a name="select-an-azure-cloud"></a>Azure クラウドを選択する

| オプション | 情報 | 説明 |
|--------|-------------|-------------|
| 名前 | **Azure China Cloud** <br><br> **Azure Cloud** <br><br> **Azure German Cloud** <br><br> **Azure US Government** <br><br> **Custom** | リソースの検出と管理を行うために Management Studio から接続する Azure クラウドを選択します。 独自の URL と DNS サフィックスを指定するには、 **[カスタム]** を選択します。 |

## <a name="service-addresses"></a>サービス アドレス

| オプション | 情報 | 説明 |
|--------|-------------|-------------|
| Azure Data Lake サービス エンドポイント | `azuredatalakeanalytics.net` | Azure Data Lake Analytics カタログとジョブ エンドポイントのサフィックスを指定します。 |
| Azure Data Lake Store ファイル システム エンドポイント | `azuredatalakestore.net` | Azure Data Lake Store ファイル システム エンドポイントのサフィックスを指定します。 | 
| Azure Key Vault 対象ユーザー | `https://vault.azure.net` | Key Vault サービスの要求を承認するアクセス トークンの対象ユーザーを指定します。 |
| Azure Key Vault DNS サフィックス | `vault.azure.net` | Azure Key Vault サーバーのドメイン名サフィックスを指定します。 |
| SQL Database DNS サフィックス | `database.windows.net` | Azure SQL Database サーバーのドメイン名サフィックスを指定します。 |
| ストレージ エンドポイント | `core.windows.net` | ストレージ アクセスのエンドポイントを指定します。 オプションには、BLOB、テーブル、キュー、ファイル ストレージなどがあります。 |
| Traffic Manager DNS サフィックス | `trafficmanager.net` | Azure Traffic Manager サービスのドメイン名サフィックスを指定します。 |