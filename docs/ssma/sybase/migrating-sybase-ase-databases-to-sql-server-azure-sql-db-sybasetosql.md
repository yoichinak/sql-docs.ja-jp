---
title: Sybase ASE データベースを SQL Server に移行する-Azure SQL Database |Microsoft Docs
description: この推奨プロセスを使用して、SQL Server Migration Assistant (SSMA) を使用して SQL Server または Azure SQL Database に SAP Adaptive Server Enterprise データベースを移行します。
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f37f80cda41279b7c773d7a2c89216c5f24e9000
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034983"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>SQL Server Azure SQL Database への SAP ASE データベースの移行 (SybaseToSQL)
SAP Adaptive Server Enterprise (ASE) の SQL Server Migration Assistant (SSMA) は、SAP ASE データベースをまたは Azure SQL Database に迅速に移行するのに役立つ包括的な環境です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 SSMA for SAP ASE を使用することにより、データベースオブジェクトとデータを確認し、データベースの移行を評価し、データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に移行した後、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に移行できます。  
  
## <a name="recommended-migration-process"></a>推奨される移行プロセス  
オブジェクトとデータを SAP ASE データベースからまたは Azure SQL Database に正常に移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次の手順を使用します。  
  
1.  [新しい SSMA プロジェクトを作成](working-with-ssma-projects-sybasetosql.md)します。  
  
    プロジェクトを作成した後、プロジェクトの変換、移行、および種類のマッピングオプションを設定できます。 プロジェクト設定の詳細については、「 [SybaseToSQL&#41;&#40;プロジェクトオプションの設定 ](../../ssma/sybase/setting-project-options-sybasetosql.md)」を参照してください。 データ型マッピングのカスタマイズの詳細については、「 [SQL&#41;の SYBASE ASE と SQL Server のデータ &#40;型のマッピング ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)」を参照してください。  
  
2.  [SAP ASE データベースサーバーに接続](connecting-to-sybase-ase-sybasetosql.md)します。  
  
3.  [インスタンス SQL Server に接続する](connecting-to-sql-server-sybasetosql.md) か [、Azure SQL Database のインスタンスに接続](connecting-to-azure-sql-db-sybasetosql.md)します。  
  
4.  [SAP ASE データベーススキーマを SQL Server/Azure SQL Database データベーススキーマにマップ](./mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)します。  
  
5.  必要に応じて、 [評価レポートを作成](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) して、データベースオブジェクトの変換を評価し、変換時間を見積もることができます。  
  
6.  [SAP ASE データベーススキーマを SQL Server/Azure SQL Database スキーマに変換](./converting-sybase-ase-database-objects-sybasetosql.md)します。  
  
7.  [変換されたデータベースオブジェクトを SQL Server/Azure SQL Database に読み込み](./loading-converted-database-objects-into-sql-server-sybasetosql.md)ます。  
  
    スクリプトを保存して、または Azure SQL Database に実行するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースオブジェクトを同期します。  
  
8.  [SQL Server/Azure SQL Database にデータを移行](./migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)します。  
  
9. 必要に応じて、データベースアプリケーションを更新します。  
  
## <a name="see-also"></a>関連項目  
[SSMA for SAP ASE のインストール &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[SSMA for SAP ASE のはじめに &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
