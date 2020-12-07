---
description: パッケージ オブジェクトの再利用
title: パッケージ オブジェクトの再利用 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- GUID regenerating [Integration Services]
- reusing packages
- templates [Integration Services]
- copying packages
- regenerating package GUID
ms.assetid: 08f723bf-15b5-44bd-9a46-04e8781bfbfb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f3ce79b8cc4d0a8fff0dda5bf833f918285eb4c7
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192439"
---
# <a name="reuse-of-package-objects"></a>パッケージ オブジェクトの再利用

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  多くの場合、パッケージには、再利用できるような機能が含まれています。 たとえば、一連のタスクを作成した場合、それらのアイテムを合わせてグループとして再利用したり、別の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトで作成した接続マネージャーのように、1 つのアイテムを再利用したりすることができます。  
  
## <a name="copy-and-paste"></a>コピーと貼り付け  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] と [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでは、制御フロー アイテム、データ フロー アイテム、接続マネージャーなど、パッケージ オブジェクトのコピーと貼り付けがサポートされます。 コピーと貼り付けは、プロジェクト間およびパッケージ間で行うことができます。 複数のプロジェクトがソリューションに含まれている場合、プロジェクト間でコピーを実行でき、それらのプロジェクトの種類は異なってもかまいません。  
  
 1 つのソリューションに複数のパッケージが含まれている場合、それらのパッケージ間でコピーと貼り付けを行うことができます。 パッケージは、同じ [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに含まれていても、異なる Integration Services プロジェクトに含まれていてもかまいません。 ただし、パッケージ オブジェクトは他のオブジェクトに依存し、その依存関係がなければ成立しない場合があります。 たとえば、SQL 実行タスクは接続マネージャーを使用します。タスクを正しく機能させるには、この接続マネージャーもコピーする必要があります。 また、パッケージ オブジェクトによっては、特定のオブジェクトが既にパッケージに含まれている必要があるものもあります。このオブジェクトがなければ、コピーしたオブジェクトをパッケージに正常に貼り付けることができません。 たとえば、1 つもデータ フロー タスクを含まないパッケージには、データ フローを貼り付けることはできません。  
  
 同じパッケージを何度もコピーして使用する場合もあります。 このようなコピー プロセスを回避するには、そのパッケージをテンプレートとして指定すれば、新しいパッケージを作成するときに使用できます。  
  
 パッケージ オブジェクトをコピーすると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] により、新しい GUID が新しいオブジェクトの **ID** プロパティに自動的に割り当てられ、 **Name** プロパティが自動的に更新されます。  
  
 変数はコピーできません。 タスクなどのオブジェクトで変数が使用される場合は、コピー先のパッケージにその変数を再作成する必要があります。 これに対して、パッケージ全体をコピーした場合は、パッケージの変数もコピーされます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [パッケージ オブジェクトをコピーする](../integration-services/copy-package-objects.md)  
  
-   [プロジェクト アイテムをコピーする](./integration-services-ssis-projects-and-solutions.md)  
  
-   [パッケージをパッケージ テンプレートとして保存する](./save-packages.md)  
  
