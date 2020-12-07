---
title: DB2 データベースの SQL Server への移行 (DB2ToSQL) |Microsoft Docs
description: SQL Server Migration Assistant (SSMA) を使用して SQL Server または Azure SQL Database に DB2 データベースを移行するには、この推奨プロセスを使用します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e31d4b1d31cb186276d8424f8c49450cb4ce9406
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869530"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>DB2 データベースの SQL Server への移行 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) for DB2 は、DB2 データベースをまたは Azure SQL Database に迅速に移行するのに役立つ包括的な環境です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 SSMA for DB2 を使用することにより、データベースオブジェクトとデータを確認し、データベースの移行を評価したり、データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に移行したり、データをまたは Azure SQL Database に移行したりすることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 SYS スキーマとシステム DB2 スキーマは移行できないことに注意してください。  
  
## <a name="recommended-migration-process"></a>推奨される移行プロセス  
オブジェクトとデータを DB2 データベースからまたは Azure SQL Database に正常に移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次の手順を使用します。  
  
1.  [新しい SSMA プロジェクト](./new-project-db2tosql.md)。  
  
    プロジェクトを作成した後、プロジェクトの変換、移行、および種類のマッピングオプションを設定できます。 プロジェクト設定の詳細については、「 [プロジェクトの設定 &#40;変換&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md) 」および関連するセクションを参照してください。 データ型マッピングをカスタマイズする方法の詳細については、「 [MAPPING DB2 and SQL Server Data Types &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)」を参照してください。  
  
2.  [DB2 データベースに接続](./connecting-to-db2-database-db2tosql.md)します。  
  
3.  [SQL Server に接続](./connecting-to-sql-server-db2tosql.md)しています。  
  
4.  [DB2 スキーマを SQL Server スキーマにマップ](./mapping-db2-schemas-to-sql-server-schemas-db2tosql.md)します。  
  
5.  必要に応じて、 [評価レポート](./assessment-report-db2tosql.md) を使用してデータベースオブジェクトの変換を評価し、変換時間を推定します。  
  
6.  [DB2 スキーマを変換](./converting-db2-schemas-db2tosql.md)します。  
  
7.  [変換されたデータベースオブジェクトを SQL Server に読み込み](./loading-converted-database-objects-into-sql-server-db2tosql.md)ます。  
  
    これは、次の方法のいずれかで実行できます。  
  
    -   スクリプトを保存し、で実行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
    -   データベースオブジェクトを同期します。  
  
8.  [DB2 データを SQL Server に移行](./migrating-db2-data-into-sql-server-db2tosql.md)する。  
  
9. 必要に応じて、データベースアプリケーションを更新します。  
  
## <a name="see-also"></a>参照  
[SSMA for DB2 &#40;DB2ToSQL&#41;のインストール ](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[SSMA for DB2 &#40;DB2ToSQL のはじめに&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
