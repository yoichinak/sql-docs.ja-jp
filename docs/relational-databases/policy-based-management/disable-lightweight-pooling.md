---
description: 簡易プーリングの無効化
title: 簡易プーリングの無効化 | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 481bb43d-6fe5-497c-9096-971fb6bf733b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 907ea87fc66c7ac3350fc1630f71f02529528678
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88406458"
---
# <a name="disable-lightweight-pooling"></a>簡易プーリングの無効化
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このルールでは、サーバーで簡易プーリングが無効であることを確認します。 簡易プーリングを 1 に設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はファイバー モード スケジューリングに切り替わります。 ファイバー モードは、UMS ワーカーのコンテキスト切り替えがパフォーマンスの重大なボトルネックになる状況を対象としています。 この状況はまれであるため、一般的なシステムのパフォーマンスやスケーラビリティがファイバー モードで向上することはほとんどありません。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 簡易プーリング オプションは、十分なテストを行い、他のパフォーマンス チューニングのすべての機会が評価された後、使用環境においてコンテキストの切り替えが既知の問題である場合にのみ有効にする必要があります。  
  
 ルーチン処理にファイバー モード スケジューリングを使用することはお勧めしません。これは、コンテキストの切り替えがもたらす本来の利点が損なわれることでパフォーマンスが低下する場合があるためと、スレッド ローカル ストレージ (TLS) やスレッド所有オブジェクト (Win32 カーネル オブジェクトの一種であるミューテックスなど) を使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の一部のコンポーネントがファイバー モードでは正常に機能しない場合があるためです。  
  
 簡易プーリングを削除するには、次のステートメントを実行し、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]を再起動します。  
  
```sql  
sp_configure 'show advanced options', 1;  
GO  
sp_configure 'lightweight pooling', 0;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="for-more-information"></a>詳細情報  
 [lightweight pooling サーバー構成オプション](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
## <a name="see-also"></a>参照  
 [ポリシーベースの管理を使用したベスト プラクティスの監視と実行](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
