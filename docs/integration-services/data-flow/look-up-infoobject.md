---
description: '[インフォオブジェクトの参照]'
title: '[インフォオブジェクトの参照] | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7f4c132-a5ec-49d8-a964-45775432731f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 93050f2a583f3fa378778397470506787c7001f5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495867"
---
# <a name="look-up-infoobject"></a>[インフォオブジェクトの参照]

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  SAP Netweaver BW システムで定義されたインフォオブジェクトを参照する場合、 **[インフォオブジェクトの参照]** ダイアログ ボックスを使用します。 使用できるインフォオブジェクトの一覧が表示されたら目的のインフォオブジェクトを選択すると、SAP BW 変換先で関連するオプションに必要な値が設定されます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換先は、 **[インフォオブジェクトの参照]** ダイアログ ボックスを使用します。 SAP BW 変換先の詳細については、「 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[インフォオブジェクトの参照] ダイアログ ボックスを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
4.  **[接続マネージャー]** ページの **[SAP BW オブジェクトの作成]** で、以下のいずれかのオプションを選択します。  
  
    1.  **[インフォキューブ]** を選択します。 **[作成]** をクリックします。 **[トランザクション データのインフォキューブの作成]** ダイアログ ボックスで、一覧のいずれかの行から **[IObject]** 列の **[検索]** をクリックします。 各行は、パッケージのデータ フローの列を表します。  
  
    2.  **[インフォソース]** を選択します。 次に、**[作成]** をクリックします。 **[インフォソースの作成]** ダイアログ ボックスで、 **[トランザクション データ]** を選択します。 **[トランザクション データのインフォソースの作成]** ダイアログ ボックスで、一覧のいずれかの行から **[IObject]** 列の **[検索]** をクリックします。 各行は、パッケージのデータ フローの列を表します。  
  
    3.  **[インフォソース]** を選択します。 次に、**[作成]** をクリックします。 **[インフォソースの作成]** ダイアログ ボックスで、 **[マスター データ]** を選択します。 **[マスター データのインフォソースの作成]** ダイアログ ボックスで、 **[参照]** をクリックします。  
  
 **[インフォオブジェクトの参照]** ダイアログ ボックスは、 **[新しいインフォオブジェクトの作成]** ダイアログ ボックスの **[属性]** セクションで **[追加]** をクリックして開くこともできます。  
  
## <a name="lookup-options"></a>[参照] のオプション  
 参照フィールドで、アスタリスクのワイルドカード文字 (*) を使用して、または部分的な文字列をアスタリスクのワイルドカード文字と組み合わせて使用して、結果をフィルター処理できます。 ただし、参照フィールドを空にした場合、参照処理は、フィールドの空の文字列のみを検索します。  
  
 **特性**  
 特性を表すインフォオブジェクトを参照します。  
  
 **ユニット**  
 単位を表すインフォオブジェクトを参照します。  
  
 **主要データ**  
 主要データを表すインフォオブジェクトを参照します。  
  
 **時間の特性**  
 時間の特性を表すインフォオブジェクトを参照します。  
  
 **Name**  
 参照するインフォオブジェクトの名前、または部分的な名前をアスタリスクのワイルドカード文字 (*) と入力します。 すべてのインフォオブジェクトを含めるには、アスタリスクのワイルドカード文字を単独で使用します。  
  
 **説明**  
 アスタリスクのワイルドカード文字 (*) と一緒に説明、または部分的な説明を入力します。 説明にかからわずすべてのインフォオブジェクトを含めるには、アスタリスクのワイルドカード文字を単独で使用します。  
  
 **[参照]**  
 SAP Netweaver BW システムで定義されている一致するインフォオブジェクトを参照します。  
  
## <a name="lookup-results"></a>参照結果  
 [参照] ボタンをクリックすると、SAP Netweaver BW システムのインフォオブジェクトの一覧が、次の列見出しのテーブルに表示されます。  
  
 **インフォオブジェクト**  
 SAP Netweaver BW システムで定義されたインフォオブジェクトの名前を表示します。  
  
 **テキスト (短い)**  
 インフォオブジェクトに関連付けられた短いテキストを表示します。  
  
 使用できるインフォオブジェクトの一覧が表示されたら目的のインフォオブジェクトを選択すると、変換先で関連するオプションに必要な値が設定されます。  
  
## <a name="see-also"></a>参照  
 [[トランザクション データのインフォキューブの作成]](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [[インフォソースの作成]](../../integration-services/data-flow/create-infosource.md)   
 [トランザクション データのインフォソースの作成](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [マスター データのインフォソースの作成](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [新しいインフォオブジェクトの作成](../../integration-services/data-flow/create-new-infoobject.md)   
 [SAP BW 変換先エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
