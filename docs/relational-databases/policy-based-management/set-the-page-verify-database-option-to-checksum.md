---
title: PAGE_VERIFY データベース オプションを CHECKSUM に設定 | Microsoft Docs
description: PAGE_VERIFY オプションが CHECKSUM であるかどうかを確認します。これは、SQL Server データベース エンジンがデータ ファイルの整合性を提供するためにチェックサムを計算するかどうかを制御します。
ms.custom: ''
ms.date: 08/19/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4dda2b9138882490b1556b9dbb39f71e35767f5f
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646512"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>PAGE_VERIFY データベース オプションを CHECKSUM に設定
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このルールでは、PAGE_VERIFY データベース オプションが CHECKSUM に設定されているかどうかを確認します。 PAGE_VERIFY データベース オプションに対して CHECKSUM を有効にすると、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ではページをディスクに書き込む際に、ページ全体の内容のチェックサムを計算し、ページ ヘッダーに計算したチェックサムの値を格納します。 このページがディスクから読み取られるときに、チェックサムが再計算され、ページ ヘッダーに格納されているチェックサムの値と比較されます。 これにより、高レベルなデータ ファイル整合性が提供されます。  データベースに対して PAGE VERIFY CHECKSUM オプションを使用した場合、ページがディスクに書き込まれた後にページが変更されたことが SQL Server で検出されると、SQL Server によってページがディスクから読み戻された後、[メッセージ 824](../errors-events/mssqlserver-824-database-engine-error.md)が報告されます。 
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 PAGE_VERIFY データベース オプションを CHECKSUM に設定します。 PAGE_VERIFY CHECKSUM データベース オプションの使用は、システム I/O パスが原因で発生するデータベースの一貫性の問題を検出するための最も強力な方法です。
  
## <a name="for-more-information"></a>詳細情報  
 [ALTER DATABASE SET のオプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
