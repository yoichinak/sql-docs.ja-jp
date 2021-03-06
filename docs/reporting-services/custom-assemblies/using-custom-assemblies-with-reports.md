---
title: レポートでのカスタム アセンブリの使用 | Microsoft Docs
description: レポート定義ファイル内からアセンブリを参照できるように、Microsoft .NET Framework を利用し、カスタム コード アセンブリを開発します。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 19977f4a90ecfb8db81c53aebf7b7ee3e4be68ca
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100064497"
---
# <a name="using-custom-assemblies-with-reports"></a>レポートでのカスタム アセンブリの使用
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポート アイテムの値、スタイル、および書式設定に関するカスタム コードを記述できます。 たとえば、カスタム コードを使用して、ロケールに基づいて通貨を書式設定したり、特殊な書式設定の特定の値にフラグを設定したり、または企業で実際に使用している他のビジネス ルールを適用したりすることができます。 このコードをご自分のレポートに含める方法の 1 つは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] を使用してお使いのレポート定義ファイルから参照できるカスタム コード アセンブリを作成することです。 サーバーは、レポートを実行するときにカスタム アセンブリの関数を呼び出します。 カスタム アセンブリは、レポートで使用する特別な関数を取得するときに使用できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [RDL ファイルのアセンブリの参照](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
 レポート定義言語ファイルのカスタム アセンブリを参照する方法について説明します。  
  
 [カスタム アセンブリの配置](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
 カスタム アセンブリをレポート デザイナーとレポート サーバーに配置する方法について説明します。  
  
 [複雑な名前を持つカスタム アセンブリの使用](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)  
 複雑な名前を持つカスタム アセンブリの使用方法について説明します。  
  
 [カスタム アセンブリでの権限のアサート](../../reporting-services/custom-assemblies/asserting-permissions-in-custom-assemblies.md)  
 カスタム アセンブリの権限を限定して配置する方法と権限をコード内でアサートする方法について説明します。  
  
 [式を使用したカスタム アセンブリへのアクセス](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)  
 カスタム アセンブリ メソッドをレポート定義のレポート式として呼び出す方法について説明します。  
  
 [カスタム アセンブリ オブジェクトの初期化](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)  
 レポートから呼び出されたカスタム アセンブリ オブジェクトの値を初期化する方法について説明します。  
  
 [方法: カスタム アセンブリをデバッグする](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 カスタム アセンブリ コードのデバッグ方法について説明します。  
  
## <a name="see-also"></a>参照  
 [レポート定義言語 &#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
