---
description: Analysis Services のアップグレード
title: Analysis Services のアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
author: Minewiskan
ms.author: owend
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: erikre
ms.openlocfilehash: 1bf7bb7c42a9172148ccdf551eed0b62b3cf5938
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670985"
---
# <a name="upgrade-analysis-services"></a>Analysis Services のアップグレード

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  Analysis Services インスタンスを同じサーバー モードの SQL Server バージョンにアップグレードすると、「[Analysis Services の新機能](/analysis-services/what-s-new-in-analysis-services)」で説明する、最新リリースで導入された機能を利用できます。  
  
 同じハードウェアで実行されている他のインスタンスとは独立して、各インスタンスをインプレース アップグレードできます。 ほとんどの管理者は、実稼働ワークロードを新しいサーバーに転送する前にアプリケーションをテストするために、新しいバージョンの新しいインスタンスをインストールしますが、 開発サーバーやテスト サーバーでは、インプレース アップグレードの方が便利な場合があります。  
  
## <a name="server-upgrade"></a>サーバーのアップグレード  
 サーバーとデータベースをアップグレードする場合、次の 2 つの基本的な方法があります。  
  
> [!NOTE]
> 特定のサーバーに接続されているデータベースの互換性レベルは、手動で変更しない限り、同じレベルのままになります。
   
  
### <a name="in-place-upgrade"></a>一括アップグレード  
 アップグレード プロセスは、既存のデータベースを古いインスタンスから新しいインスタンスに自動的に移行します。 メタデータおよびバイナリ データは 2 つのバージョン間で互換性があるため、アップグレード後もそのまま使用できます。手動でデータを移行する必要はありません。  
  
 既存のインスタンスをアップグレードするには、セットアップを実行し、新しいインスタンスの名前として既存のインスタンス名を指定します。  
  
### <a name="side-by-side-upgrade"></a>サイド バイ サイド アップグレード  
  
-   すべてのデータベースをバックアップし、それぞれ復元できることを確認します。 詳しくは、「[Analysis Services データベースのバックアップと復元](/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)」をご覧ください。  
  
-   アップグレード後のサーバーの動作を確認するための基礎として後で使用する、レポート、スプレッドシート、またはダッシュ ボード スナップショットのサブセットを特定します。 可能であれば、アップグレードしたサーバーで同じワークロードを比較できるように、パフォーマンス測定値を収集します。  
  
-   置き換えるサーバーと同じサーバー モード (表形式または多次元) を選択して、Analysis Services の新しいインスタンスをインストールします。 
  
     インストール後のタスクに従って、ポートを構成し、サーバー管理者を追加します。 詳しくは、「[インストール後の構成 &#40;Analysis Services&#41;](/analysis-services/instances/post-install-configuration-analysis-services)」をご覧ください。  
  
-   各データベースを接続または復元します。  
  
-   DBCC を実行して、データベースの整合性をチェックします。 表形式モデルでは、モデル階層全体にわたって孤立したオブジェクトがないかどうかをテストして、徹底したチェックが行われます。 多次元モデルでは、パーティション インデックスだけがチェックされます。 詳しくは、「[Analysis Services の表形式および多次元データベース用 Database Consistency Checker &#40;DBCC&#41;](/analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services)」をご覧ください。  
  
-   レポート、スプレッドシート、ダッシュボードをテストして、動作や計算に問題となるような変化がないことを確認します。 多次元と表形式のどちらのワークロードでも、パフォーマンスが向上していることを確認する必要があります。  
  
-   ログインやアクセス許可の問題を解決して、処理動作をテストします。 接続に既定のサービス アカウントを使用している場合、新しいサービスは別のアカウントで実行されます。 詳しくは、「[サービス アカウントの構成 &#40;Analysis Services&#41;](/analysis-services/instances/configure-service-accounts-analysis-services)」をご覧ください。  
  
-   新しいサーバー名を使用するようにスクリプトを調整して、アップグレードされたサーバーでバックアップおよび復元操作をテストします。  
  
## <a name="database-upgrade"></a>データベースのアップグレード  
 以前のバージョンで作成されたデータベースは、アップグレード後のサーバー上で、基のデータベース互換性レベルの設定を使って実行されます。 一般に、新機能にアクセスできるようにするために、データベースまたはモデルをアップグレードして、より高い互換性レベルで運用できますが、これを行うと、サーバーの特定のバージョンにバインドされることに注意してください。  
  
 データベースをアップグレードするには、通常、SQL Server Data Tools (SSDT) でモデルをアップグレードし、アップグレードされたサーバー インスタンスにソリューションを展開します。
  
 表形式データベースと多次元データベースは、異なるバージョン パスに従います。 多次元モデルと表形式モデルの互換性レベルが似た値になるのは偶然です。  機能の変更がどちらか一方にのみ影響する場合、モードは異なる速度で進歩することになります。  
  
 基礎知識を得るために、次の表には互換性レベルがまとめられていますが、詳細記事を確認して、各レベルが提供する機能を把握する必要があります。  
  
|データベース モデル|互換性レベル|互換性のあるバージョン|  
|-|-|-|  
|表形式|1400|SQL Server 2017|
|表形式|1200|SQL Server 2016|  
|表形式|1103|SQL Server 2014|  
|表形式|1100|SQL Server 2012|  
|多次元|1100|SQL Server 2012 以降|  
|多次元|1050|SQL Server 2005、2008、2008 R2|  
  
 詳しくは、「[多次元データベースの互換性レベル &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services)」および「[Compatibility level for Analysis Services tabular models](/analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services)」(Analysis Services 表形式モデルの互換性レベル) をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server のインストール計画](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Power Pivot for SharePoint のアップグレード](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
  
