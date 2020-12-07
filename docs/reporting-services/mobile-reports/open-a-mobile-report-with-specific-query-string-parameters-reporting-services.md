---
title: 特定のクエリ文字列パラメーターを使用してモバイル レポートを開く | Microsoft Docs
description: パラメーターとデータ ソースを含む Reporting Services モバイル レポートでは、レポート URL にクエリ パラメーターを使用して、指定した値で開くことができます。
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: abcdda5a396451508df78610eeb4f7bc417484d5
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907350"
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>特定のクエリ文字列パラメーターを使用してモバイル レポートを開く | Reporting Services
パラメーターを含む [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] モバイル レポートと、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] のデータ ソースがある場合、レポート URL にクエリ文字列パラメーターを追加して、指定した値を自動的に付けて開くようにすることができます。 
1.  [パラメーターを使用するモバイル レポート](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)を作成します。

2. Mobile Report Publisher を開き、[データ] タブを選択します。 

2. タブのテーブルの下部で、データセットの名前と必要なフィールド名を検索します。 
    
    ![モバイル レポートの発行者パラメーター データ ビューのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  URL の構文は、データ ソースによって異なります。 

     **SQL Server Analysis Services のデータ ソースの場合** :次の形式で、クエリ文字列パラメーターを含む URL を作成します。

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    次に例を示します。
    
    `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **SQL Server のデータ ソースの場合** :クエリ文字列パラメーターはほとんど同様ですが、フィールド名の前に \@ 記号を付けます。

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    次に例を示します。
    
      `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  この URL を使用すると、サーバーでレポートが開き、指定したパラメーター値で自動的にフィルター処理されます。

    ![URL とこのテキスト "?TimeChartLoD.@category=Clothing" を囲む枠を指す矢印がある、モバイル レポートの発行者パラメーターの Web ポータル ビューのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>関連項目

[モバイル レポートにパラメーターを追加する](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

