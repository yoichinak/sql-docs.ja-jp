---
title: SQL Server のプロパティ ([Always On 高可用性] タブ)
description: 高可用性およびディザスター リカバリーのソリューションとして可用性グループを使用するには、SQL Server の Always On 可用性グループ機能を有効にします。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c67f5f1e1021a303a1cdb52e02fdb5c8c1f8f2e2
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901544"
---
# <a name="sql-server-properties-always-on-high-availability-tab"></a>SQL Server のプロパティ ([Always On 高可用性] タブ)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  **構成マネージャーの** [SQL Server のプロパティ] **ダイアログ ボックスの** [Always On 高可用性] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] タブを使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の Always On 可用性グループを有効または無効にします。 Always On 可用性グループの有効化は、高可用性およびディザスター リカバリー ソリューションとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが可用性グループを使用するための前提条件です。  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 Always On 可用性グループを有効にするには、サーバー インスタンスが以下の前提条件を満たしている必要があります。  
  
-   このサーバー インスタンスは、Windows Server フェールオーバー クラスタリング (WSFC) ノードに存在している必要があります。  
  
-   同じ可用性グループのインスタンスはすべて、同じ WSFC クラスターに属している必要があります。 可用性グループが複数の WSFC クラスターにまたがることはできません。  
  
-   サーバー インスタンスでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をサポートする [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]エディションを実行する必要があります。  
  
-   一度に 1 つのサーバー インスタンスでのみ Always On 可用性グループを有効にします。 Always On 可用性グループを有効にした後は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが再起動するまで待ってから、次のサーバー インスタンスを有効にしてください。  
  
> [!NOTE]  
>  サポートされている機能の詳細、および [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]の追加の前提条件、制限、推奨設定については、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] オンライン ブックをご覧ください。  
  
## <a name="dialog-options"></a>ダイアログ オプション  
 **[Windows フェールオーバー クラスター名]**  
 ローカル コンピューターのノードが含まれる WSFC クラスターの名前が表示されます。  
  
 **AlwaysOn 可用性グループを有効にする**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスで Always On 可用性グループを有効または無効にするには、このチェック ボックスを使用します。  
  
-   このチェック ボックスがオフの場合、Always On 可用性グループは現在無効になっています。 Always On 可用性グループを有効にするには、このチェック ボックスをオンにして、 **[OK]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを手動で再起動します。  
  
-   このチェック ボックスが既にオンに設定されている場合、Always On 可用性グループは現在有効になっています。 Always On 可用性グループを無効にするには、このチェック ボックスをオフにし、 **[OK]** をクリックします。 これにより、サーバー インスタンスが再起動します。  
  
    > [!TIP]  
    >  Always On 可用性グループを無効にした後は、サーバー インスタンスからローカル可用性レプリカをすべて削除する必要があります。 各可用性グループの最後のレプリカを削除したら、グループも削除する必要があります。  
  
## <a name="ui-element-list"></a>UI 要素の一覧  
  
> [!NOTE]  
>  Always On 可用性グループを無効にした後の設定と、可用性グループの作成および構成方法については、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] オンライン ブックをご覧ください。  
  
  
