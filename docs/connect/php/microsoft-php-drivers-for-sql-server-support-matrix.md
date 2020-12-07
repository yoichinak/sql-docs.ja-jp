---
title: Microsoft Drivers for PHP のサポート マトリックス
description: このページには、Microsoft SQL Server 用 PHP Driver のサポート表とサポート ライフサイクル ポリシーがあります。
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 778d9aa4ee666ba3719095508d5f5e28516f954d
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942161"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>SQL Server 用 Microsoft PHP Drivers のサポート マトリックス

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このページには、Microsoft SQL Server 用 PHP Driver のサポート表とサポート ライフサイクル ポリシーがあります。

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP Drivers サポート ライフサイクルのマトリックスとポリシー

マイクロソフト サポート ライフサイクル (MSL) ポリシーでは、マイクロソフト製品のサポート ライフサイクルを理解しやすくする、予測可能な情報を提供しています。 PHP ドライバーのバージョン 3.x、4.x、5.x には、ドライバーのリリース日から 5 年間のメインストリーム サポートが含まれています。 メインストリーム サポートについては、[マイクロソフト サポート ライフサイクルの Web サイト](https://support.microsoft.com/lifecycle)で定義されています。

延長サポートとカスタム サポートのオプションは、Microsoft PHP Driver では使用できません。

次の Microsoft PHP Driver は、表示されているサポートの終了日までサポートされます。

|ドライバー名|ドライバー パッケージのバージョン|メインストリーム サポートの終了|
|-|:-:|-|
|SQL Server 用 Microsoft PHP ドライバー 5.8|5.8|2025 年 1 月 31 日|
|SQL Server 用 Microsoft PHP ドライバー 5.6|5.6|2024 年 2 月 21 日|
|SQL Server 用 Microsoft PHP ドライバー 5.3|5.3|2023 年 7 月 20 日|
|SQL Server 用 Microsoft PHP ドライバー 5.2|5.2|2023 年 2 月 9 日|
|SQL Server 用 Microsoft PHP ドライバー 4.3|4.3|2022 年 7 月 6 日|
|SQL Server 用 Microsoft PHP ドライバー 4.0|4.0|2021 年 7 月 11 日|
|SQL Server 用 Microsoft PHP ドライバー 3.2|3.2|2020 年 3 月 9 日|
| &nbsp; | &nbsp; | &nbsp; |

次の Microsoft PHP ドライバーはサポートされなくなりました。

|ドライバー名|ドライバー パッケージのバージョン|メインストリーム サポートの終了|
|-|:-:|-|
|SQL Server 用 Microsoft PHP ドライバー 3.1|3.1|2019 年 12 月 12日|
|SQL Server 用 Microsoft PHP ドライバー 3.0|3.0|2017 年 3 月 6 日|
|SQL Server 用 Microsoft PHP ドライバー 2.0|2.0|2015 年 8 月 10 日|
|SQL Server 用 Microsoft PHP ドライバー 1.0|1.0|2014 年 4 月 28 日|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>SQL Server バージョンの認定済み互換性
 次のマトリックスは、対応するドライバー バージョンと互換性があることをテストおよび認定済みのデータベース バージョンを示しています。 Microsoft は、以前のバージョンのドライバーとの下位互換性を維持することに努めていますが、サポートされている最新のドライバーのみが、SQL Server のリリース時に新しい SQL Server バージョンでテストおよび認定されます。

|ドライバー バージョン&nbsp;&#8594;<br />&#8595; データベース バージョン|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL データベース        |はい|はい|はい|はい|[はい]|   |   |
|Azure SQL Managed Instance|○|はい|はい|はい|はい|   |   |
|Azure Synapse Analytics   |はい|はい|はい|はい|はい|   |   |
|SQL Server 2019           |はい|   |   |   |   |   |   |
|SQL Server 2017           |はい|はい|はい|はい|はい|   |   |
|SQL Server 2016           |はい|はい|はい|はい|はい|はい|   |
|SQL Server 2014           |はい|はい|はい|はい|はい|はい|はい|
|SQL Server 2012           |はい|はい|はい|はい|はい|はい|はい|
|SQL Server 2008 R2        |   |はい|はい|はい|はい|はい|はい|
|SQL Server 2008           |   |   |   |   |   |はい|はい|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

Azure SQL Database での PHP の使用の詳細については、「[Microsoft Azure SQL Database への接続](connecting-to-microsoft-azure-sql-database.md)」を参照してください。

## <a name="php-version-support"></a>PHP バージョンのサポート

次のバージョンの PHP は、Microsoft PHP ドライバーの一覧に示したバージョンでサポートされています。

|ドライバー バージョン&nbsp;&#8594;<br />&#8595; PHP バージョン|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|:---:|---|---|---|---|---|---|---|
|7.4|7.4.0+          |                |                |                |       |        |        |
|7.3|7.3.0+          |7.3.0+          |                |                |       |        |        |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |        |        |
|7.1|                |7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |        |        |
|7.0|                |                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+  |        |
|5.6|                |                |                |                |       |        |5.6.4+  |
|5.5|                |                |                |                |       |        |5.5.16+ |
|5.4|                |                |                |                |       |        |5.4.32  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. バージョン 7.2.1 以降は Windows でサポートされており、バージョン 7.2.0 以降は Linux および macOS でサポートされています。

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

次のバージョンの Windows オペレーティング システムは、Microsoft PHP ドライバーの一覧に示したバージョンでサポートされています。

|ドライバー バージョン&nbsp;&#8594;<br />&#8595; オペレーティング システム|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2019                 |はい|はい|   |   |   |   |   |
|Windows Server 2016                 |はい|はい|はい|はい|はい|   |   |
|Windows Server 2012 R2              |はい|はい|はい|はい|はい|はい|はい|
|Windows Server 2012                 |はい|はい|はい|はい|はい|はい|はい|
|Windows Server 2008 R2 SP1          |   |   |   |   |   |はい|はい|
|Windows Server 2008 R2              |   |   |   |   |   |   |   |
|Windows Server 2008 SP2             |   |   |   |   |   |はい|はい|
|Windows 10                          |はい|はい|はい|はい|はい|はい|   |
|Windows 8.1                         |はい|はい|はい|はい|はい|はい|はい|
|Windows 8                           |   |   |   |   |はい|はい|はい|
|Windows 7 SP1                       |   |   |   |   |   |はい|はい|
|Windows Vista SP2                   |   |   |   |   |   |はい|はい|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

次のバージョンの Linux および macOS オペレーティング システム (64 ビットのみ) は、Microsoft PHP ドライバーの一覧に示したバージョンでサポートされています。

|ドライバー バージョン&nbsp;&#8594;<br />&#8595; オペレーティング システム|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 20.04 (64 ビット)               |はい|   |   |   |   |   |   |
|Ubuntu 19.10 (64 ビット)               |はい|   |   |   |   |   |   |
|Ubuntu 18.10 (64 ビット)               |   |はい|   |   |   |   |   |
|Ubuntu 18.04 (64 ビット)               |はい|はい|はい|   |   |   |   |
|Ubuntu 17.10 (64 ビット)               |   |   |はい|はい|   |   |   |
|Ubuntu 16.04 (64 ビット)               |はい|はい|はい|はい|はい|はい|   |
|Ubuntu 15.10 (64 ビット)               |   |   |   |   |はい|   |   |
|Ubuntu 15.04 (64 ビット)               |   |   |   |   |   |はい|   |
|Debian 10 (64 ビット)                  |はい|   |   |   |   |   |   |
|Debian 9 (64 ビット)                   |はい|はい|はい|はい|   |   |   |
|Debian 8 (64 ビット)                   |はい|はい|はい|はい|はい|   |   |
|Red Hat Enterprise Linux 8 (64 ビット) |はい|   |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 ビット) |はい|はい|はい|はい|はい|はい|   |
|Suse Enterprise Linux 15 (64 ビット)   |はい|はい|   |   |   |   |   |
|Suse Enterprise Linux 12 (64 ビット)   |はい|はい|はい|はい|   |   |   |
|Alpine Linux 3.11 (64 ビット)<sup>1</sup>|はい|   |   |   |   |   |   |
|macOS Catalina (64 ビット)             |はい|   |   |   |   |   |   |
|macOS Mojave (64 ビット)               |はい|はい|   |   |   |   |   |
|macOS High Sierra (64 ビット)          |はい|はい|はい|   |   |   |   |
|macOS Sierra (64 ビット)               |   |はい|はい|はい|はい|   |   |
|macOS El Capitan (64 ビット)           |   |   |はい|はい|はい|   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> Alpine Linux サポートは、バージョン 5.8.0 では試験段階です。 バージョン 5.8.1 では、実稼働サポートが導入されます。

## <a name="see-also"></a>参照

[リリース ノート](release-notes-php-sql-driver.md)

[サポート リソース](support-resources-for-the-php-sql-driver.md)

[システム要件](system-requirements-for-the-php-sql-driver.md)
