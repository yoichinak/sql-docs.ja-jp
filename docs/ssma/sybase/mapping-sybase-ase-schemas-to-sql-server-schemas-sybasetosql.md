---
description: Sybase ASE スキーマの SQL Server スキーマへのマッピング (SybaseToSQL)
title: Sybase ASE スキーマを SQL Server スキーマにマップする (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a0084551b2e1ab6de4c3731f33525ccd3a8a48d5
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100017527"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Sybase ASE スキーマの SQL Server スキーマへのマッピング (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) では、各データベースに1つ以上のスキーマがあります。 既定では、SSMA は、データベース内のすべてのオブジェクトとスキーマを、または SQL Azure の同じデータベースおよびスキーマに移行し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 ただし、ASE と Azure SQL Database の間のマッピングをカスタマイズすることはでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE および SQL Server または SQL Azure スキーマ  
ASE と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure は、両方とも *データベース* とそのスキーマを指定します。これは、2つの部分で構成されるスキーマとして使用します。 たとえば、ASE **デモ** データベースでは、 **dbo** スキーマが存在する可能性があります。 そのデータベースとスキーマのペアは、 **demo. dbo** として指定されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure に同じデータベースとスキーマが指定されている場合は、そのペアも **demo. dbo** として指定されます。  
  
## <a name="modifying-the-target-database-and-schema"></a>ターゲットデータベースとスキーマの変更  
SSMA では、ASE スキーマを任意の使用可能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure スキーマにマップできます。  
  
**データベースとスキーマを変更するには**  
  
1.  Sybase メタデータエクスプローラーで、[ **データベース**] を選択します。  
  
    [ **スキーママッピング** ] タブは、個々のデータベース、 **スキーマ** フォルダー、または個々のスキーマを選択した場合にも使用できます。 [ **スキーママッピング** ] タブの一覧は、選択したオブジェクトに合わせてカスタマイズされています。  
  
2.  右ペインで、[ **スキーママッピング** ] タブをクリックします。  
  
    すべての ASE データベースとそのスキーマとターゲット値の一覧が表示されます。 このターゲットは、または SQL Azure の2つの部分表記 (*データベーススキーマ*) で表され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトとデータが移行されます。  
  
3.  変更するマッピングを含む行を選択し、[ **変更**] をクリックします。  
  
4.  [ **ターゲットスキーマの選択** ] ダイアログボックスで、使用可能なターゲットデータベースとスキーマを参照するか、2つの部分表記 (データベーススキーマ) のテキストボックスにデータベースとスキーマ名を入力し、[ **OK**] をクリックします。  
  
5.  [ **スキーママッピング** ] タブでターゲットが変更されます。  
  
**マッピングのモード**  
  
-   SQL Server へのマッピング  
  
ソースデータベースを任意のターゲットデータベースにマップできます。 既定では、ソースデータベースは SSMA を使用して接続したターゲットデータベースにマップされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 マップされているターゲットデータベースがに存在しない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"データベースまたはスキーマがターゲットメタデータに存在しません" というメッセージが表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。同期中に作成されます。続行しますか? "** [はい] をクリックします。 同様に、スキーマを、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同期中に作成されるターゲットデータベース下に存在しないスキーマにマップすることもできます。  
  
-   SQL Azure へのマッピング  
  
接続先のターゲット Azure SQL Database、または接続されているターゲット Azure SQL Database 内の任意のスキーマに、ソースデータベースをマップできます。 送信元スキーマを [接続されたターゲットデータベース] の既存ではないスキーマにマップすると、 **"スキーマはターゲットメタデータに存在しません" というメッセージが表示されます。同期中に作成されます。続行しますか?[はい] をクリックし** ます。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>既定のデータベースとスキーマに戻す  
ASE スキーマとまたは SQL Azure スキーマ間のマッピングをカスタマイズする場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マッピングを既定値に戻すことができます。  
  
**既定のデータベースとスキーマに戻すには**  
  
1.  [スキーママッピング] タブで、任意の行を選択し、[既定 **値にリセット** ] をクリックして既定のデータベースとスキーマに戻します。  
  
## <a name="next-steps"></a>次の手順  
Sybase ASE オブジェクトからオブジェクトへの変換または SQL Azure オブジェクトへの変換を分析する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [変換レポートを作成](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)できます。 それ以外の場合は [、ASE データベースオブジェクト定義](converting-sybase-ase-database-objects-sybasetosql.md) を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure オブジェクト定義に変換できます。  
  
## <a name="see-also"></a>参照  
[Sybase ASE データベースを SQL Server Azure SQL Database &#40;SybaseToSQL&#41;に移行する ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
