---
description: DQS クレンジング接続マネージャー
title: DQS クレンジング接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: faa1eedd-db14-41e5-8e58-8f0f6f561e42
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dc0bb9e5238e490689b9ffa57836d2db0666e75b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100338437"
---
# <a name="dqs-cleansing-connection-manager"></a>DQS クレンジング接続マネージャー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  DQS クレンジング接続マネージャーを使用すると、パッケージから [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] サーバーに接続できます。 DQS クレンジング変換では、DQS クレンジング接続マネージャーを使用します。  
  
 Data Quality Services について詳しくは、「 [Data Quality Services の概念](../../data-quality-services/data-quality-services-concepts.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  DQS クレンジング接続マネージャーでは、Windows 認証のみがサポートされています。  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティについて詳しくは、「 [[DQS クレンジング変換エディター] ダイアログ ボックス](../data-flow/transformations/dqs-cleansing-transformation.md)」をご覧ください。  
  
 プログラムによる接続マネージャーの構成については、開発者ガイドの <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> クラスのドキュメントをご覧ください。  
  
