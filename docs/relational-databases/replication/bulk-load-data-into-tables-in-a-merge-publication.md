---
description: マージ パブリケーションでのテーブルへのデータの一括読み込み
title: マージ パブリケーションでのテーブルへのデータの一括読み込み | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8d94dba664453cc559133c6dad1bc4fce7eada45
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455644"
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication"></a>マージ パブリケーションでのテーブルへのデータの一括読み込み
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [bcp ユーティリティ](../../tools/bcp-utility.md)または [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) コマンドを使用してテーブルにデータを読み込むと、既定では、[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) システム テーブル内の追跡データを維持するマージ レプリケーション トリガーが起動されなくなります。 データが読み込まれたときにマージ レプリケーション トリガーを強制的に起動するか、一括コピー操作の後にレプリケーション ストアド プロシージャを使用して、生成されたレプリケーション メタデータをプログラムによって挿入できます。  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>マージ レプリケーションによってパブリッシュされたテーブルに bcp ユーティリティを使用してデータを一括読み込みするには  
  
1.  マージ レプリケーションを使用してパブリッシュされたテーブルにデータを挿入するには、パブリッシャーまたはサブスクライバーで [bcp Utility](../../tools/bcp-utility.md) または [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) を実行します。  
  
2.  挿入されたデータ用のレプリケーション メタデータが生成されようにするには、次のいずれかの方法を使用します。  
  
    -   FIRE_TRIGGERS オプションを使用して一括コピーを実行する。  
  
    -   データの挿入先のデータベースで、[sp_addtabletocontents &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md) を実行する。 `@table_name` には、データが挿入されたテーブルの名前を指定します。  
  
  
