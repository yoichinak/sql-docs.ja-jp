---
title: RDL ファイルのアセンブリの参照 | Microsoft Docs
description: レポート定義言語 (RDL) ファイルでアセンブリを参照する方法について説明します。特に、CodeModules 要素と Classes 要素を取り上げます。
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6d27d3f44d9b60a2c3bb38249881d38adbc6f2e2
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100064507"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>RDL ファイルのアセンブリの参照
  レポート定義ファイルでのカスタム コード アセンブリの使用をサポートするため、2 つのレポート定義言語 (RDL) 要素 **CodeModules** と **Classes** が RDL 仕様に含まれています。  
  
 **CodeModules** 要素を使用すると、レポート式でマネージド コード アセンブリを参照できます。 **CodeModules** は、レポート定義ファイルで特殊な関数の呼び出しに使用するアセンブリへの参照を含むトップレベルの要素です。 カスタム アセンブリの使用をサポートするレポート定義のエントリは次のようになります。  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 カスタム コードから <xref:System.Reflection.Assembly.Load%2A> を呼び出すのではなく、**CodeModule** 要素を RDL ファイルに手動で追加するか、 **[レポートのプロパティ]** ダイアログの **[参照]** タブを使用してカスタム アセンブリを登録します。 詳細については、「 [レポート デザイナーでカスタム コードやアセンブリを式から参照する (SSRS)](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)を表しています。  
  
 **Classes** 要素では、レポート定義でのインスタンス メンバーの使用がサポートされます。 **Classes** は、クラス名とインスタンス名への参照を含むトップレベルの要素です。 インスタンス メンバーの使用をサポートするレポート定義のエントリは次のようになります。  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 詳細については、「[式を使用したカスタム アセンブリへのアクセス](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポートでのカスタム アセンブリの使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
