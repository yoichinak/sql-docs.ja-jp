---
title: 方法:カスタム レポート アイテムを配置する | Microsoft Docs
description: カスタム レポート アイテムを配置する方法について説明します。 レポート サーバー構成ファイルを変更し、コンポーネント アセンブリを適切なフォルダーにコピーします。
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 240be4e7d05e4daac27e15bf5f8a99ec6bc27563
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100061907"
---
# <a name="how-to-deploy-a-custom-report-item"></a>方法:カスタム レポート アイテムを配置する
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] でカスタム レポート アイテムを配置するには、レポート サーバー構成ファイルを変更し、デザイン時と実行時のコンポーネント アセンブリをレポート デザイナーとレポート サーバーの両方に対する適切なアプリケーション フォルダーにコピーする必要があります。  
  
### <a name="to-deploy-a-custom-report-item"></a>カスタム レポート アイテムを配置するには  
  
1.  Rsreportdesigner.config ファイルを編集して、デザイナーで使用するカスタム レポート アイテムの実行時とデザイン時のコンポーネントを構成します。 **ReportItemName** エントリは、**CustomReportItemDesigner** クラスで使用される **CustomReportItemAttribute** 属性と一致する必要があることにご注意ください。 次に例を示します。  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    <ReportItemDesigner>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsDesigner, PolygonsDesigner" />  
    </ReportItemDesigner>  
    <ReportItemConverter>  
       <Converter Source="Chart" Target="Polygons" Type="PolygonsCRI.PolygonsConverter, PolygonsDesigner" />  
    </ReportItemConverter>  
    ```  
  
2.  Rsreportserver.config ファイルを編集して、カスタム レポート アイテムの実行時コンポーネントを登録します。 次に例を示します。  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  Rsssrvpolicy.config ファイルを編集して、カスタム レポート アイテムに適切なアクセス許可を付与する **CodeGroup** を追加します。 次に例を示します。  
  
    ```  
    <CodeGroup   
       class="UnionCodeGroup"   
       version="1"   
       PermissionSetName="FullTrust"  
       Description="This code group grants MyCustomReportItem.dll FullTrust permission. ">  
       <IMembershipCondition   
          class="UrlMembershipCondition"  
          version="1"  
       Url="C:\Program Files\Microsoft SQL Server\ MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin\MyCustomReportItem.dll" />  
    </CodeGroup>  
    ```  
  
4.  カスタム レポート アイテムの実行時コンポーネント DLL を、%ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies ディレクトリと \Program Files\Microsoft SQL Server\MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin ディレクトリにコピーします。  
  
5.  カスタム レポート アイテムのデザイン時コンポーネント DLL を %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies ディレクトリにコピーします。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [カスタム レポート アイテムのクラス ライブラリ](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
