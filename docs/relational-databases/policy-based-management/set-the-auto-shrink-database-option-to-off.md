---
description: AUTO_SHRINK データベース オプションを OFF に設定
title: AUTO_SHRINK データベース オプションを OFF に設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9a8815d5958ca8cb2aabb498636c631eb91744d8
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596744"
---
# <a name="set-the-auto_shrink-database-option-to-off"></a>AUTO_SHRINK データベース オプションを OFF に設定
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このルールでは、AUTO_SHRINK データベース オプションが OFF に設定されているかどうかをチェックします。 データベースの圧縮と拡張により、物理的な断片化が発生することがよくあります。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 AUTO_SHRINK データベース オプションを OFF に設定します。 再利用している領域が今後不要になることがわかっている場合は、データベースを手動で圧縮して領域を再利用できます。  
  
## <a name="for-more-information"></a>詳細情報  
 サポート技術情報の資料 [315512](/troubleshoot/sql/admin/considerations-autogrow-autoshrink)  
  
## <a name="see-also"></a>参照  
 [ポリシーベースの管理を使用したベスト プラクティスの監視と実行](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
