---
description: SQL Server の各エディションがサポートする Integration Services の機能
title: SQL Server の各エディションがサポートする Integration Services の機能 | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b5cb516c1d7058d455919a3faffed5b653a1bae6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449877"
---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>SQL Server の各エディションがサポートする Integration Services の機能

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


 このトピックでは、 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]のさまざまなエディションでサポートされる SQL Server Integration Services (SSIS) の機能の詳細について説明します。  

Evaluation Edition と Developer Edition でサポートされている機能については、下の表に記載されている Enterprise Edition の機能をご覧ください。
  
最新のリリース ノートと新機能については、以下の記事を参照してください。
-   [SQL Server 2016 リリース ノート](../sql-server/sql-server-2016-release-notes.md)
-   [SQL Server 2016 の Integration Services の新機能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [SQL Server 2017 の Integration Services の新機能](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**SQL Server 2016 をお試しください。**    

180 日の試用期間中、SQL Server Evaluation Edition をご利用いただけます。  
    
> [![Evaluation Center からダウンロードする](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[Evaluation Centerから SQL Server 2016 をダウンロードする](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="new-integration-services-features-in-sql-server-2017"></a><a name="ISNew"></a> SQL Server 2017 の新しい Integration Services 機能
  
|特徴量|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Scale Out Master|はい|||||
|Scale Out Worker|はい|はい <sup>1</sup>|TBD|TBD|TBD|
|OData コンポーネントで Microsoft Dynamics AX および Microsoft Dynamics CRM をサポート <sup>2</sup>|はい|はい||||
|Linux Support|はい|はい|||はい|

<sup>1</sup> Scale Out で Enterprise のみの機能を必要とするパッケージを実行する場合は、Scale Out Worker を SQL Server Enterprise のインスタンスでも実行する必要があります。

<sup>2</sup> この機能は、SQL Server 2016 Service Pack 1 でもサポートされています。

## <a name="sql-server-import-and-export-wizard"></a><a name="IEWiz"></a> SQL Server インポートおよびエクスポート ウィザード

|特徴量|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Server インポートおよびエクスポート ウィザード|はい|はい|はい|可<sup>1</sup>|可<sup>1</sup>|

<sup>1</sup> DTSWizard.exe は、Linux 上の SQL には用意されていません。 ただし、Linux 上の dtexec を、Windows 上の DTSWizard によって作成されたパッケージを実行するために使用できます。


## <a name="integration-services"></a><a name="IS"></a> Integration Services  
  
|特徴量|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|組み込みのデータ ソース コネクタ|はい|はい|||| 
|組み込みのタスクと変換|はい|はい||||  
|ODBC のソースとターゲット |はい|はい|||| 
|Azure データ ソース コネクタおよびタスク|はい|はい||||  
|Hadoop/HDFS コネクタおよびタスク|はい|はい||||  
|基本的なデータ プロファイリング ツール|はい|はい|||| 

## <a name="integration-services---advanced-sources-and-destinations"></a><a name="ISAA"></a> Integration Services – 高度なソース/ターゲット  
  
|特徴量|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Attunity 高パフォーマンス Oracle ソース/ターゲット|はい|||||  
|Attunity 高パフォーマンス Teradata ソース/ターゲット|はい|||||  
|SAP BW 変換元と変換先|はい|||||  
|データ マイニング モデル トレーニング変換先|はい|||||  
|ディメンション処理変換先|はい|||||  
|パーティション処理変換先|はい|||||  
  
## <a name="integration-services---advanced-tasks-and-transformations"></a><a name="ISAT"></a> Integration Services - 高度なタスクおよび変換  
  
|特徴量|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Attunity 変更データ キャプチャ コンポーネント <sup>1</sup>|はい|||||  
|データ マイニング クエリ変換|はい|||||  
|あいまいグループ化とあいまい参照変換|はい|||||  
|用語抽出および用語参照変換|はい|||||  

<sup>1</sup> Attunity 変更データ キャプチャ コンポーネントには Enterprise Edition が必要です。 ただし、Change Data Capture Service と Change Data Capture Designer では Enterprise Edition は不要です。 Designer および Service は、SSIS がインストールされていないコンピューターで使用できます。
