---
description: 特定の種類のデータ フロー コンポーネントの開発
title: 特定の種類のデータ フロー コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 28f31c63139ddd5ce6b09933411cb600e246de53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484285"
---
# <a name="developing-specific-types-of-data-flow-components"></a>特定の種類のデータ フロー コンポーネントの開発

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  このセクションでは、変換元コンポーネント、同期出力型変換コンポーネント、非同期出力型変換コンポーネント、および変換先コンポーネントの開発の詳細について説明します。  
  
 コンポーネント開発全般の詳細については、「[カスタム データ フロー コンポーネントの開発](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [カスタム変換元コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 外部データ ソースのデータにアクセスし、そのデータをデータ フローの下流コンポーネントに提供するコンポーネントの開発について説明します。  
  
 [同期出力型のカスタム変換コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 入力に同期して出力する変換コンポーネントの開発について説明します。 これらのコンポーネントは、データ フローにデータを追加せず、データが渡されるたびに処理を行います。  
  
 [非同期出力型のカスタム変換コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 出力が入力に同期しない変換コンポーネントの開発について説明します。 これらのコンポーネントは、上流コンポーネントからデータを受け取ると共に、データをデータ フローに追加します。  
  
 [カスタム変換先コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 データ フローの上流コンポーネントから行を受け取り、外部データ ソースに書き込むコンポーネントの開発について説明します。  
  
## <a name="reference"></a>リファレンス  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 カスタム データ フロー コンポーネントを作成するために使用するクラスやインターフェイスが含まれています。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 データ フロー タスクのアンマネージ クラスやアンマネージ インターフェイスを示します。 プログラムによってデータ フローを構築する場合、またはカスタム データ フロー コンポーネントを作成する場合、開発者はこれらを使用します。また、マネージド <xref:Microsoft.SqlServer.Dts.Pipeline> 名前空間も同じ目的で使用されます。  
  
## <a name="see-also"></a>参照  
 [スクリプティング ソリューションとカスタム オブジェクトとの比較](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [特定の種類のスクリプト コンポーネントの開発](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
