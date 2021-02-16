---
title: SQL Server Integration Services (SSIS) Scale Out | Microsoft Docs
description: この記事では、SQL Server Integration Services (SSIS) Scale Out 機能の概要を提供します。この機能は、SSIS パッケージの実行パフォーマンスを高めます
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9e75be10cff0f34d132ecfe57ddff10538091a77
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100338363"
---
# <a name="integration-services-ssis-scale-out"></a>Integration Services (SSIS) Scale Out

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


SQL Server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) Scale Out では、パッケージの実行を複数のコンピューターに分散することにより、SSIS パッケージの実行パフォーマンスを高めます。 Scale Out をセットアップしたら、SQL Server Management Studio (SSMS) から、複数のパッケージ実行を並列にスケールアウト モードで実行することができます。

## <a name="components"></a>Components
[!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out は、1 つの [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out Master と 1 つ以上の [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out Worker で構成されます。

-   Scale Out Master は、Scale Out の管理を担当し、ユーザーからパッケージの実行要求を受け取ります。 詳細については、[Scale Out Master](integration-services-ssis-scale-out-master.md) に関するページを参照してください。

-   Scale Out Worker は、Scale Out Master から実行作業をプルし、パッケージを実行します。 詳細については、[Scale Out Worker](integration-services-ssis-scale-out-worker.md) に関するページを参照してください。

## <a name="configuration-options"></a>構成オプション
Scale Out は、次の構成でセットアップすることができます。

-   **1 台のコンピューター**。この場合、Scale Out Master と Scale Out Worker が同じコンピューター上で並行して実行されます。

-   **複数のコンピューター**。この場合、各 Scale Out Worker は、別々のコンピューター上にあります。

## <a name="what-you-can-do"></a>実行可能な操作
Scale Out をセットアップすると、次のことができます。

-   SSISDB カタログに配置された複数のパッケージを実行します。 詳細については、「[Integration Services (SSIS) Scale Out でパッケージを実行する](run-packages-in-integration-services-ssis-scale-out.md)」をご覧ください。

-   Scale Out Manager アプリで、Scale Out トポロジを管理します。 詳細については、「[Integration Services Scale Out](integration-services-ssis-scale-out-manager.md)」をご覧ください。

## <a name="next-steps"></a>次のステップ
-   [1 台のコンピューターでの Integration Services (SSIS) Scale Out の概要](get-started-with-ssis-scale-out-onebox.md)

-   [チュートリアル: Integration Services Scale Out をセットアップする](walkthrough-set-up-integration-services-scale-out.md)
