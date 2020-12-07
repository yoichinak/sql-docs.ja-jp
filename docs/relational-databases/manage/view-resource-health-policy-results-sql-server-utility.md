---
title: リソース正常性ポリシーの結果の表示 (SQL Server ユーティリティ) | Microsoft Docs
description: SQL Server Management Studio を使用して、SQL Server およびデータ層アプリケーションのインスタンスに関する SQL Server ユーティリティのリソース正常性ポリシーの結果を表示する方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a3ec26ba8988f36e3deac88373a932ef377f8d59
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810035"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>リソース正常性ポリシーの結果の表示 (SQL Server ユーティリティ)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスおよびデータ層アプリケーションに関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのリソース パラメーターを表示するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でユーティリティのダッシュボードを使用します。 詳細については、「 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。  

##  <a name="SSMSProcedure"></a>

### <a name="view-sql-server-utility-resource-health-policy-results"></a>SQL Server ユーティリティのリソース正常性ポリシーの結果の表示  

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で、 **[表示]** 、 **[ユーティリティ エクスプローラー]** を順に選択して、ユーティリティ エクスプローラーのナビゲーション ウィンドウを表示します。 **[表示]** 、 **[ユーティリティ エクスプローラーのコンテンツ]** を順に選択し、コンテンツ ウィンドウを表示します。  

2. ナビゲーション ウィンドウで、![[ユーティリティへの接続]](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility") **[ユーティリティへの接続]** を選択します。 ユーティリティ コントロール ポイント (UCP) を作成していない場合、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスまたはデータ層アプリケーションを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録していない場合は、「 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。  

3. UCP ノードを選択し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスおよびデータ層アプリケーションの概要データを表示します (更新するには右クリックします)。 ダッシュボードのデータは、コンテンツ ウィンドウに表示されます。  

4. **[マネージド インスタンス]** ノードを選択し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスのリスト ビュー データを表示します (更新するには右クリックします)。 リスト ビューのデータは、コンテンツ ウィンドウに表示されます。  

5. **[配置済みのデータ層アプリケーション]** ノードを選択し、データ層アプリケーションのリスト ビュー データを表示します (更新するには右クリックします)。 リスト ビューのデータは、コンテンツ ウィンドウに表示されます。  

## <a name="see-also"></a>参照

- [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [CPU 使用率のポリシーにおけるノイズの軽減 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)
- [配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130))
- [マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ&#41;](./utility-explorer-f1-help.md)
- [ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))