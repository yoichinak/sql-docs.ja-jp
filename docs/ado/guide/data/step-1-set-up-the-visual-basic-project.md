---
description: 手順 1:Visual Basic プロジェクトを設定する
title: '手順 1: Visual Basic プロジェクトを設定する |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: rothja
ms.author: jroth
ms.openlocfilehash: b80f44160e3542147158f0bece7c87adb3ba7e4f
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032444"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>手順 1:Visual Basic プロジェクトを設定する
このシナリオでは、Microsoft Visual Basic 6.0、ADO 2.5 以降、および Microsoft OLE DB Provider for Internet Publishing がシステムにインストールされていることを前提としています。 最初に新しいプロジェクトを作成し、次にプロジェクトの既定のフォームにコントロールを追加します。  
  
### <a name="to-create-an-ado-project"></a>ADO プロジェクトを作成するには:  
  
1.  Microsoft Visual Basic で、新しい標準 EXE プロジェクトを作成します。  
  
2.  [プロジェクト] メニューの [参照] をクリックします。  
  
3.  [Microsoft ActiveX データオブジェクト2.5 ライブラリ] を選択し、[OK] をクリックします。  
  
### <a name="to-insert-controls-on-the-main-form"></a>メインフォームにコントロールを挿入するには、次の操作を行います。  
  
1.  Form1 に ListBox コントロールを追加します。 Name プロパティを **lstMain** に設定します。  
  
2.  Form1 に別の ListBox コントロールを追加します。 Name プロパティを **lstDetails** に設定します。  
  
3.  Form1 に TextBox コントロールを追加します。 Name プロパティを **Txtdetails** に設定します。  
  
## <a name="see-also"></a>参照  
 [インターネット公開のシナリオ](../../../ado/guide/data/internet-publishing-scenario.md)   
 [手順 2:Main リスト ボックスを初期化する](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
