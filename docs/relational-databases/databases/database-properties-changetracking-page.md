---
title: '[データベースのプロパティ] ([変更の追跡] ページ) | Microsoft Docs'
description: '[データベースのプロパティ] ダイアログ ボックスの [ChangeTracking] タブを使用して、データベースの変更追跡の設定を表示または変更する方法について説明します。'
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7129094815add7f3f49aaa5e99b353b3f656a848
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193022"
---
# <a name="database-properties-changetracking-page"></a>[データベースのプロパティ] ([変更の追跡] ページ)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  このページを使用すると、選択されているデータベースの変更の追跡設定を表示または変更できます。 このページで使用可能なオプションの詳細については、「[変更の追跡の有効化と無効化 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)」を参照してください。  
  
## <a name="options"></a>Options  
 **変更の追跡**  
 データベースの変更の追跡の有効/無効を切り替えます。  
  
 変更の追跡を有効にするには、データベースを変更する権限が必要です。  
  
 この値を **True** に設定すると、個々のテーブルで変更の追跡を有効にできるデータベース オプションが設定されます。  
  
 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)を使用して変更追跡を構成することもできます。  
  
 **保有期間**  
 データベースに変更追跡情報を保持する最低限の期間を指定します。 データは、 **[自動クリーンアップ]** の値が **True** の場合にのみ削除されます。  
  
 既定値は 2 です。  
  
 **[保有期間の単位]**  
 保有期間の値の単位を指定します。 **[日]** 、 **[時間]** 、または **[分]** を選択できます。 既定値は **[日]** です。  
  
 最小保有期間は 1 分です。 最大保有期間はありません。  
  
 **[自動クリーンアップ]**  
 指定した保有期間を過ぎると変更追跡情報が自動的に削除されるかどうかを指定します。  
  
 **[自動クリーンアップ]** を有効にすると、以前のカスタム保有期間はすべて既定の保有期間 (2 日) にリセットされます。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)  
  
