---
title: SQL Server のリソース正常性のトラブルシューティング (SQL Server ユーティリティ) | Microsoft Docs
description: SQL Server UCP によって特定されるリソース正常性の問題のトラブルシューティングについて説明します。これには、CPU の過大使用、ファイル領域、割り当てられたディスク領域などがあります。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c6c6d499d485941d490848b68b5c8142edd0cb4b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810690"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>SQL Server のリソース正常性のトラブルシューティング (SQL Server ユーティリティ)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP によって特定されるリソース正常性の問題のトラブルシューティングでは、コンピューターや [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスでの CPU の過大使用を緩和したり、データ層アプリケーションの CPU の過大使用を緩和したりします。 この他にも、データベース ファイルのファイル領域の過大使用や記憶域ボリュームに割り当てられたディスク領域の過大使用の解決も行われます。  
  
 データベースが "緊急" 状態になっている場合、正常性状態は過大使用になっているログ ファイル領域を示します。  
  
 データ収集の失敗 (UCP のマネージド インスタンスのリスト ビューに灰色の状態アイコンで示されます) の詳細については、「 [SQL Server ユーティリティのトラブルシューティング](/previous-versions/sql/sql-server-2016/ee210592(v=sql.130))」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの概要の詳細については、「 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP で検出された特定のリソースの正常性に関する問題を緩和する方法の詳細については、以下のトピックを参照してください。  
  
-   [SQL Server のバージョンとエディションを識別する方法](https://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [SQL Server 2008 のパフォーマンスに関する問題のトラブルシューティング](/previous-versions/sql/sql-server-2008/dd672789(v=sql.100))  
  
