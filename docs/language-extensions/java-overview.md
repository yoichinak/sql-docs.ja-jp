---
title: Java 言語拡張とは
titleSuffix: SQL Server Language Extensions
description: Java 言語拡張は、外部 Java コードの実行に使用される SQL Server の機能です。 機能拡張フレームワークを使用する外部 Java コードで、リレーショナル データを使用できます。
author: dphansen
ms.author: davidph
ms.date: 11/10/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 4df5f2e96ff8795ac592c6aa61f7c79e03145c31
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596297"
---
# <a name="what-is-java-language-extension"></a>Java 言語拡張とは
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

Java 言語拡張は、外部 Java コードの実行に使用される SQL Server の機能です。 [機能拡張フレームワーク](concepts/extensibility-framework.md)を使用する外部 Java コードで、リレーショナル データを使用できます。 Java 言語拡張は、[SQL Server 言語拡張](language-extensions-overview.md)の一部です。

既定の Java ランタイムは Zulu Open JRE です。 別の Java JRE または SDK を使用することもできます。

## <a name="what-you-can-do-with-the-java-language-extension"></a>Java 言語拡張でできること

Java 言語拡張では、外部コードを実行するために拡張機能フレームワークが使用されます。 コードの実行はコア エンジン プロセスから分離されていますが、SQL Server のクエリ実行と完全に統合されています。 データのソースで Java コードを実行できるため、ネットワーク経由でデータをプルする必要はありません。

外部 Java 言語は [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) で定義されます。 Java コードを実行するためのインターフェイスとして、システム ストアド プロシージャ [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) が使用されます。

## <a name="get-started-with-java-language-extension"></a>Java 言語拡張の使用を開始する

1. [SQL Server の Java 言語拡張を Windows 上にインストール](install/windows-java.md)するか [Linux 上にインストール](../linux/sql-server-linux-setup-language-extensions-java.md)します。

1. 開発ツールを構成します。

    + Java コードの開発には、好みの IDE を使用します。
    + [Microsoft Extensibility SDK for Java](how-to/extensibility-sdk-java-sql-server.md) をインストールして、SQL Server 上で Java コードを実行します
    + SQL Server 上で外部コードを実行するために、[Azure Data Studio](../azure-data-studio/what-is-azure-data-studio.md) を使用します。
    + システム ストアド プロシージャ [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して SQL Server 上で Java コードを実行します。

1. 最初の Java コードを記述します。

    + [チュートリアル:Java での正規表現](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>制限事項

入力および出力バッファーの値の数は、Java の配列に割り当てることができる要素の最大数であるため、`MAX_INT (2^31-1)` を超えることはできません。

## <a name="next-steps"></a>次のステップ

+ [SQL Server の Java 言語拡張を Windows 上にインストール](install/windows-java.md)するか [Linux 上にインストール](../linux/sql-server-linux-setup-language-extensions-java.md)する
+ [Microsoft 拡張機能 SDK for Java](how-to/extensibility-sdk-java-sql-server.md) をインストールします