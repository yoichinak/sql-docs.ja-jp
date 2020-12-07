---
title: SQL Server 言語拡張の新機能
titleSuffix: ''
description: 外部言語とデータ プラットフォームの間の統合を拡張、拡大、強化する SQL Server 言語拡張の新機能について説明します。
author: dphansen
ms.author: davidph
ms.date: 11/09/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0b1f7aec4b3581a8604fad68518a36ac8ecc14dd
ms.sourcegitcommit: 863420525a1f5d5b56b311b84a6fb14e79404860
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94417999"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>SQL Server 言語拡張の新機能
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

外部言語とデータ プラットフォーム間の統合が継続的に拡大、拡張、および強化されており、各リリースで[言語拡張](language-extensions-overview.md)機能が SQL Server に追加されています。

## <a name="sql-server-2019"></a>SQL Server 2019

SQL Server 2019 の[言語拡張](language-extensions-overview.md)の新機能については、以下を参照してください。 このリリースのすべての機能の詳細については、[SQL Server 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md)に関するページ、および「[SQL Server 2019 のリリース ノート](../sql-server/sql-server-version-15-release-notes.md)」を参照してください。

### <a name="new-python-and-r-language-extensions"></a>新しい Python と R の言語拡張機能

- 言語拡張で、[Python カスタム ランタイム](../machine-learning/install/custom-runtime-python.md)を使用できます。 詳細については、[Windows に Python カスタム ランタイムをインストールする](../machine-learning/install/custom-runtime-python.md?view=sql-server-ver15&preserve-view=true)か [Linux に Python カスタム ランタイムをインストールする](../machine-learning/install/custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true)ための方法を参照してください。

- 言語拡張で [R カスタム ランタイム](../machine-learning/install/custom-runtime-r.md)を利用できます。 詳細については、[Windows に R カスタム ランタイムをインストールする](../machine-learning/install/custom-runtime-r.md?view=sql-server-ver15&preserve-view=true)か [Linux に R カスタム ランタイムをインストールする](../machine-learning/install/custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true)ための方法を参照してください。

### <a name="new-java-language-extension"></a>新しい Java の言語拡張機能

- Windows および Linux の既定の Java ランタイムは Open Zulu JRE であり、[Windows 上の SQL Server 言語拡張のインストール](install/windows-java.md)と [Linux 上の SQL Server 言語拡張のインストール](../linux/sql-server-linux-setup-language-extensions-java.md)に含まれています。
- サポートされている [Java データ型](how-to/java-to-sql-data-types.md)。
- SQL Server で外部言語 (Java など) を登録するための [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)。
- [Microsoft 拡張機能 SDK for Java](how-to/extensibility-sdk-java-sql-server.md)。
- Windows および Linux 上では、外部ライブラリで [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) ステートメントを使用して Java コードにアクセスできます。 詳細情報:[SQL Server から Java を呼び出す方法](how-to/call-java-from-sql.md)。
- Windows および Linux 上の [Java 言語拡張](language-extensions-overview.md)。 アクセス許可を割り当て、パスを設定することで、コンパイル済みの Java コードを SQL Server で使用できるようになります。 SQL Server にアクセスできるクライアント アプリでは、[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を呼び出すことで、データを使用し、コードを実行することができます。これは、SQL Server Machine Learning Services 上での R と Python の統合に使用されるものと同じ手順です。

## <a name="next-steps"></a>次のステップ

+ [Windows 上](install/windows-java.md)または [Linux 上に SQL Server 言語拡張をインストール](../linux/sql-server-linux-setup-language-extensions-java.md)します。
