---
description: 列コピー変換
title: 列コピー変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
- sql13.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 27673de93d920cdc6adddd12deadcdc4a774d86c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194144"
---
# <a name="copy-column-transformation"></a>列コピー変換

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  列コピー変換は、入力列をコピーして新しい列を変換出力に追加し、新しい列を作成します。 後のデータ フローで、その列コピーに別の変換を適用できます。 たとえば、列コピー変換を使用して列のコピーを作成した後、文字マップ変換を使用してそのコピーしたデータを大文字に変換したり、集計変換を使用して新しい列に集計を適用したりできます。  
  
## <a name="configuration-of-the-copy-column-transformation"></a>列コピー変換の構成  
 列コピー変換を構成するには、コピーする入力列を指定します。 一度の操作で、1 列の複数コピー、または複数列の複数コピーを作成できます。  
  
 この変換は 1 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](../set-the-properties-of-a-data-flow-component.md)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="copy-column-transformation-editor"></a>列コピー変換エディター
  **[列コピー変換エディター]** ダイアログ ボックスを使用すると、コピーする列を選択して、新しい出力列に名前を割り当てることができます。  
  
> [!NOTE]  
>  すべての変換元データを変換先へ単にコピーする場合、列コピー変換を使用する必要がないことがあります。 データ変換が不要な場合、状況によっては変換元を変換先に直接接続できます。 このような場合は、SQL Server インポートおよびエクスポート ウィザードを使用してパッケージを作成することをお勧めします。 パッケージでは、必要に応じて、後から機能強化や再構成が可能です。 詳細については、「 [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 チェック ボックスを使用して、コピーする列を選択します。 選択した列が入力列として下のテーブルに追加されます。  
  
 **入力列**  
 使用できる入力列の一覧からコピーする列を選択します。 選択内容が **[使用できる入力列]** テーブルのチェック ボックスに反映されます。  
  
 **[出力の別名]**  
 新しい出力列の別名をそれぞれ入力します。 既定では、入力列の名前の後に「 **のコピー**」と付きます。一意のわかりやすい名前を付けることもできます。  
  
## <a name="see-also"></a>参照  
 [データ フロー](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
