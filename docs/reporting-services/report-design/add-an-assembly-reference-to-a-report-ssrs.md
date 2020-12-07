---
title: レポートにアセンブリへの参照を追加する | Microsoft Docs
description: レポート ビルダーで、レポート プロセッサで名前を解決できるよう、レポートへのアセンブリ参照を提供する方法について説明します。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 34bc95e7b07e7d248018de5ab187699964987fac
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934827"
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>レポートにアセンブリへの参照を追加する (SSRS)
  <xref:System.Math> または <xref:System.Convert> にない [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クラスへの参照を含むカスタム コードを埋め込む場合は、レポート プロセッサで名前を解決できるように、レポートへのアセンブリ参照を指定する必要があります。 詳細については、「[レポートにコードを追加する (SSRS)](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)」を参照してください。  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>レポートにアセンブリへの参照を追加するには  
  
1.  **[デザイン]** ビューで、デザイン画面のレポートの罫線の外を右クリックし、 **[レポートのプロパティ]** をクリックします。  
  
2.  **[参照]** をクリックします。  
  
3.  **[アセンブリの追加または削除]** で **[追加]** をクリックしてから、参照ボタンをクリックし、アセンブリを参照します。  
  
4.  **[クラスの追加または削除]** で **[追加]** をクリックしてから、クラスの名前を入力し、レポート内で使用するインスタンス名を指定します。  
  
    > [!NOTE]  
    >  インスタンスベースのメンバーにのみ、クラスおよびインスタンスの名前を指定してください。 **[クラス]** の一覧に静的メンバーを指定しないでください。 詳細については、「 [レポート デザイナーでカスタム コードやアセンブリを式から参照する (SSRS)](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)を表しています。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [レポートでのカスタム アセンブリの使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [[参照] ([レポートのプロパティ] ダイアログ ボックス)](./custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)  
  
