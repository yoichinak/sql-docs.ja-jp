---
title: 使用状況データ コレクションとクラッシュ レポートを有効または無効にする
description: この記事では、使用状況とクラッシュ レポートのデータが収集されて Microsoft に送信されるかどうかを制御する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: ee687a6c6ab63386ad0e96e97ea86397703b53d1
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100040522"
---
# <a name="enable-or-disable-usage-data-collection-for-azure-data-studio"></a>Azure Data Studio のデータ コレクションを有効または無効にする

## <a name="how-to-disable-telemetry-reporting"></a>テレメトリ レポートを無効にする方法

Azure Data Studio では、使用状況データが収集されて Microsoft に送信され、製品やサービスの改善に役立てられます。 詳細については、[プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)をお読みください。

使用状況データを Microsoft に送信したくない場合は、*telemetry.enableTelemetry* 設定を *false* に設定できます。

Azure Data Studio からのすべてのテレメトリ イベントをサイレント状態にするには、 **[ファイル]**  >  **[基本設定]**  >  **[設定]** で、次のオプションを追加します。

```json
    "telemetry.enableTelemetry": false
```

**重要な注意**: このオプションを有効にするには、Azure Data Studio の再起動が必要です。 

## <a name="how-to-disable-crash-reporting"></a>クラッシュ レポートを無効にする方法

クラッシュ レポートを無効にするには、 **[ファイル]**  >  **[基本設定]**  >  **[設定]** で、次のオプションを追加します。

```json
    "telemetry.enableCrashReporter": false
```

**重要な注意**: このオプションを有効にするには、Azure Data Studio の再起動が必要です。

## <a name="additional-resources"></a>その他のリソース
- [ワークスペースとユーザー設定](settings.md)
