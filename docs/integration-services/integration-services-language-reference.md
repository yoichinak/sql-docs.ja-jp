---
description: Integration Services 言語リファレンス
title: Integration Services 言語リファレンス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 53c23b16efed8909186d17cfcfafc6e91f283ef3
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193898"
---
# <a name="integration-services-language-reference"></a>Integration Services 言語リファレンス

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  このセクションでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスに配置されている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを管理するための [!INCLUDE[tsql](../includes/tsql-md.md)] API について説明します。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] は、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログと呼ばれるデータベースにオブジェクト、設定、および業務データを格納します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログの既定の名前は、SSISDB です。 カタログに格納されているオブジェクトには、プロジェクト、パッケージ、パラメーター、環境、操作履歴があります。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログは、ユーザーに表示されない内部テーブルにデータを格納します。 ただし、必要な情報は、パブリック ビューに対してクエリを実行することで公開されます。 カタログの一般的なタスクを実行するために使用できる一連のストアド プロシージャも用意されています。  
  
 通常、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] を開くことによって、カタログの [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] オブジェクトを管理します。 ただし、データベース ビューとストアド プロシージャを直接使用することも、マネージド API を呼び出すカスタム コードを記述することもできます。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] およびマネージド API では、ビューに対してクエリを実行し、多くのタスクを実行するストアド プロシージャ (このセクションで説明) を呼び出します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ビュー &#40;Integration Services カタログ&#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 ビューに対してクエリを実行し、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] オブジェクト、設定、および業務データを調べます。  
  
 [ストアド プロシージャ &#40;Integration Services カタログ&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 ストアド プロシージャを呼び出して、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] オブジェクトおよび設定を追加、削除、または変更します。  
  
 [関数 &#40;Integration Services カタログ&#41;](./functions-dm-execution-performance-counters.md)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを管理する関数を呼び出します。  
  
