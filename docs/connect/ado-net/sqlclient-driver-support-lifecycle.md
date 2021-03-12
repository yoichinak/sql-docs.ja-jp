---
title: SqlClient ドライバーのサポート ライフサイクル
description: 製品サポート ライフサイクル情報を含むページ。
ms.date: 03/03/2021
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: 998fc5eecfa0e8840111b1ee9bf1d9e653ac5687
ms.sourcegitcommit: 15c7cd187dcff9fc91f2daf0056b12ed3f0403f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102464734"
---
# <a name="sqlclient-driver-support-lifecycle"></a>SqlClient ドライバーのサポート ライフサイクル

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft.Data.SqlClient ライブラリは、すべてのリリースで最新の .NET Core サポート ポリシーに準拠しています。

[.NET Core サポート ポリシーを表示する](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)

## <a name="microsoftdatasqlclient-release-cadence"></a>Microsoft Data SqlClient のリリース周期

新しい安定版 (GA) リリースは、バージョン 1.2 以降、定期的に 6 か月ごとに公開され、その間に 2、3 個のプレビュー リリースが公開されます。 長期サポート (LTS) リリースは、いくつかの条件とお客様の反応に基づいて、利害関係者と保守担当者が選択します。

### <a name="actively-supported-releases"></a>アクティブにサポートされているリリース

| Version | 公式リリース日 | 最新の修正プログラム バージョン | 修正プログラム リリース日 | サポート レベル  | サポートの終了 |
| -- | -- | -- | -- | -- | -- |
| 2.1 | 2020 年 11 月 19 日 | 2.1.2 | 2021 年 3 月 3 日 | LTS | 2023 年 11 月 20 日 |
| 1.1 | 2019 年 11 月 20 日 | 1.1.3 | 2020 年 5 月 15 日 | LTS | 2022 年 11 月 21 日 |

### <a name="out-of-support-releases"></a>サポート対象外のリリース

| バージョン | 最新の修正プログラム リリース日 | 最新の修正プログラム バージョン | サポート終了 |
| -- | -- | -- | -- |
| 2.0 | 2020 年 6 月 16 日 | 2.0.1 | 2020 年 8 月 25 日 |
| 1.0 | 2019 年 9 月 26 日 | 1.0.19269.1 | 2020 年 2 月 20 日 |


## <a name="azure-key-vault-provider-release-cadence"></a>Azure Key Vault プロバイダーのリリース周期

`Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider` の新しい安定した (GA) リリースは、新しい機能が追加されると必要に応じて公開されます。 長期サポート (LTS) リリースは、いくつかの条件とお客様の反応に基づいて、利害関係者と保守担当者が選択します。

### <a name="actively-supported-releases"></a>アクティブにサポートされているリリース

| Version | 公式リリース日 | 最新の修正プログラム バージョン | 修正プログラム リリース日 | サポート レベル  | サポートの終了 |
| -- | -- | -- | -- | -- | -- |
| 2.x | 2021 年 3 月 3 日 | 2.0.0 | 2021 年 3 月 3 日 | LTS | 2024 年 3 月 4 日 |
| 1.x | 2019 年 11 月 19 日 | 1.2.0 | 2020 年 12 月 1 日 | LTS | 2022 年 11 月 21 日 |


## <a name="long-term-support-lts-releases"></a>長期サポート (LTS) リリース

LTS リリースは、初回リリース後 3 年間サポートされます。

## <a name="current-releases"></a>最新リリース

最新リリースは、次の最新リリースまたは LTS リリース後 3 か月間サポートされます。


## <a name="sql-version-compatibility-with-microsoftdatasqlclient"></a>SQL バージョンと Microsoft.Data.SqlClient の互換性

|データベースのバージョン&nbsp;&#8594;<br />&#8595; ドライバーのバージョン|Azure SQL データベース|Azure Synapse Analytics|Azure SQL Managed Instance|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|
|---|---|---|---|---|---|---|---|---|
|2.1|はい|はい|はい|はい|はい|はい|はい|はい|
|2.0|はい|はい|はい|はい|はい|はい|はい|はい|
|1.1|はい|はい|はい|はい|はい|はい|はい|はい|
|1.0|はい|はい|はい|はい|はい|はい|はい|はい|

## <a name="supported-os-versions"></a>サポートされている OS のバージョン

### <a name="support-for-net-framework-applications"></a>.NET Framework アプリケーションのサポート

Microsoft.Data.SqlClient では、.NET Framework v4.6 以降でサポートされるすべてのオペレーティング システムがサポートされます。

[.NET Framework のシステム要件](/dotnet/framework/get-started/system-requirements)。

### <a name="support-for-net-core-applications"></a>.NET Core アプリケーションのサポート

Microsoft.Data.SqlClient では、.NET Core v2.1 以降でサポートされるすべてのオペレーティング システムがサポートされます。

[.NET Core でサポートされている OS ライフサイクル ポリシー](https://github.com/dotnet/core/blob/master/os-lifecycle-policy.md)。

> [!NOTE]
> 現在、グローバリゼーション インバリアント モードはサポートされていません。
