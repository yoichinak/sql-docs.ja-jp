---
title: 並列処理の最大限度と最大ポリシーベースの管理
description: SQL Server のポリシーベース管理の並列処理の最大限度値を検証するポリシーの構成について説明します。
ms.custom: seo-lt-2019
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6aada496465c642570f9b60a0b1659bbe9ee3db6
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890902"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>最適なパフォーマンスを実現するための max degree of parallelism オプションの設定
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このルールでは、値の max degree of parallelism (MAXDOP) オプションが 8 より大きいかどうかを確認します。 このオプションを大きな値に設定すると、多くの場合、不要なリソース消費やパフォーマンスの低下が発生します。  
  
## <a name="best-practice-recommendations"></a>ベスト プラクティスの推奨事項  
 max degree of parallelism (MAXDOP) 構成オプションを使用すると、並列プランでクエリを実行する場合に使用するプロセッサの個数を制御できます。 このオプションでは、並列処理を実行するクエリ プラン演算子のために使用されるスレッドの数が決定されます。 対称型マルチプロセッシング (SMP) コンピューター、Non-Uniform Memory Access (NUMA) コンピューター、またはハイパー スレッディング対応プロセッサのいずれで SQL Server が設定されているかに応じて、max degree of parallelism オプションを適切に構成する必要があります。 
 
 MAXDOP を構成する上での推奨事項は、使用されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンによって異なります。 バージョン固有のガイドラインについては、「[max degree of parallelism サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)」を参照し、max degree of parallelism の値を適宜検証するポリシーを構成してください。     
  
## <a name="for-more-information"></a>詳細情報  
 [SQL Server での max degree of parallelism configuration 構成オプションの推奨事項とガイドライン](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)    
 [max degree of parallelism サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)     
