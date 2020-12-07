---
description: レッスン 1:配置バンドルを作成する準備
title: 'レッスン 1: 配置バンドルを作成する準備 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b6fe283c-9856-4ba1-a497-e3912424fd18
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c5ef2363d07fc6560199154633fc45d93eb10c13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462003"
---
# <a name="lesson-1-preparing-to-create-the-deployment-bundle"></a>レッスン 1:配置バンドルを作成する準備

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


このレッスンでは、チュートリアルをサポートする作業フォルダーと環境変数を作成し、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成します。さらに、いくつかのパッケージとそのサポート ファイルをプロジェクトに追加し、パッケージに構成を実装します。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、プロジェクトの基本構造の上にパッケージが配置されます。したがって、配置バンドルを作成する最初のステップとして、すべてのパッケージおよびパッケージの依存関係を 1 つの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトにまとめる必要があります。 配置するパッケージに他の情報を含めると役立つことがよくあります。たとえば、このグループのパッケージに関する基本的な情報を記述した Readme ファイルもプロジェクトに追加する予定です。  
  
パッケージとファイルを追加した後、まだ構成を使用していないパッケージに構成を追加します。 構成を実装すると、パッケージとパッケージ オブジェクトのプロパティが実行時に更新されます。 後のレッスンで、パッケージの配置時にこれらの構成の値を変更して、配置先の環境でパッケージがサポートされるようにします。  
  
構成を追加した後、配置時に解決する必要がある問題をより的確に把握するために、ETL パッケージを作成するための [!INCLUDE[ssIS](../includes/ssis-md.md)] のグラフィカルなツールである [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] デザイナーでパッケージを開き、パッケージおよびパッケージの要素のプロパティと、パッケージの構成を確認してください。 たとえば、パッケージの 1 つを使用してテキスト ファイルからデータを抽出するので、配置したパッケージが正常に実行されるには、データ ファイルの場所を更新する必要があります。  
  
**このレッスンの推定所要時間:** 1 時間  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
このレッスンの内容は次のとおりです。  
  
-   [手順 1:作業フォルダーと環境変数の作成](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
-   [手順 2:配置プロジェクトの作成](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
-   [手順 3:パッケージとその他のファイルの追加](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
-   [手順 4:パッケージ構成の追加](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
-   [手順 5:更新したパッケージのテスト](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
[手順 1:作業フォルダーと環境変数の作成](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
  
  
