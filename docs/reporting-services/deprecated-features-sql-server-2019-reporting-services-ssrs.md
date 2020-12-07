---
title: SQL Server 2019 Reporting Services で非推奨の機能 | Microsoft Docs
description: この記事では、SQL Server Reporting Services の次のバージョンで非推奨となる SQL Server 2019 Reporting Services の機能について説明します。
ms.date: 08/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d3e48ab45f34e583dbbeca883a64d04dc965b018
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283819"
---
# <a name="deprecated-features-in-sql-server-2019-reporting-services"></a>SQL Server 2019 Reporting Services で非推奨の機能

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2019-and-later](../includes/ssrs-appliesto-2019-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../includes/ssrs-appliesto-pbirs.md)]

ある機能が非推奨とされた場合、次のようになります。

- その機能は保守管理状態にあり、それ以外では利用されていません。 新しい変更は行われません。新しい機能との相互運用性に関する変更もありません。
- Microsoft は、アップグレードを容易にする目的で、今後のリリースから非推奨機能を外さないように努めます。 ただし、その機能が将来の技術革新を制限してしまうような場合は、Reporting Services からそれを永久的に外すことをまれに選択することがあります。
- 新しい開発作業に非推奨機能を使用することはお勧めしません。

**SQL Server の将来のバージョンで非推奨となっている機能**

SQL Server Reporting Services では、SQL Server の次のバージョンでは以下の機能がサポートされますが、それより後のバージョンでは非推奨となる予定です。 SQL Server の具体的なバージョンはまだ決定していません。

| **カテゴリ** | **非推奨の機能** | **代替** |
| --- | --- | --- |
| レポート サーバー | レポート パーツ ギャラリー | なし |
| レポート サーバー | モバイル レポートと Mobile Report Publisher | Power BI Report Server の Power BI レポートは、モバイル機能を提供します。 |
| レポート サーバー | XLS および DOC のレンダリング フォーマット | XLSX および DOCX 形式が使用可能であり、サポートされます。 |
| レポート サーバー | Atom データ フィード | SSRS と Power BI Report Server の共有データセットで、OData フィードのサポートが使用可能です。 |
| レポート サーバー | Power BI にピン留めする | ページ分割されたレポートのサポートが Power BI サービスで直接利用できるようになりました。  |

## <a name="see-also"></a>関連項目

[SQL Server 2019 Reporting Services (SSRS) で廃止された機能](discontinued-functionality-sql-server-reporting-services-2019.md)

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
