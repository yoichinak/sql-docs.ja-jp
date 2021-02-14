---
title: MySQL データベースを SQL Server スキーマ (MySQLToSQL) にマップするにはMicrosoft Docs
description: MySQL スキーマと SQL Server または Azure SQL Database 間の SSMA for MySQL マッピングをカスタマイズする方法、または既定値をそのまま使用する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 44ac691a0fe9cb4b513a2f9b435457c699c7e3e9
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100076079"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>MySQL データベースの SQL Server スキーマへのマッピング (MySQLToSQL)
既定では、SSMA for MySQL は、MySQL スキーマ内のすべてのオブジェクトを、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スキーマに対してという名前のまたは Azure SQL Database に移行します。 ただし、MySQL スキーマと Azure SQL Database 間のマッピングをカスタマイズでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL および SQL Server または SQL Azure スキーマ  
MySQL のスキーマの概念は、データベースとそのスキーマの SQL Server 概念にマップされます。 SSMA とは、データベースとスキーマの SQL Server の組み合わせをスキーマとして表します。  
  
MySQL のスキーマの概念は、データベースとそのスキーマの SQL Server 概念にマップされます。 たとえば、MySQL には **HR** という名前のスキーマが含まれている場合があります。 SQL Server のインスタンスには、 **HR** という名前のデータベースがあり、そのデータベース内にはスキーマがあります。 1つのスキーマは、 **dbo** (またはデータベース所有者) スキーマです。 既定では、MySQL スキーマの **hr** は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースとスキーマの **hr. dbo** にマップされます。 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とは、スキーマとしてのデータベースとスキーマの組み合わせを意味します。  
  
MySQL と Azure スキーマの間のマッピングを変更でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="modifying-the-target-database-and-schema"></a>ターゲットデータベースとスキーマの変更  
SSMA では、MySQL スキーマを任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スキーマまたは SQL Azure スキーマにマップできます。  
  
**データベースとスキーマを変更するには**  
  
1.  MySQL メタデータエクスプローラーで、[ **スキーマ**] を選択します。  
  
    [ **スキーママッピング** ] タブは、個別のスキーマを選択した場合にも使用できます。 [ **スキーママッピング** ] タブの一覧は、選択したオブジェクトに合わせてカスタマイズされています。  
  
2.  右ペインで、[ **スキーママッピング** ] タブをクリックします。  
  
    すべての MySQL スキーマの一覧が表示され、その後にターゲット値が表示されます。 このターゲットは、または SQL Azure の2つの部分表記 (*データベーススキーマ*) で表され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトとデータが移行されます。  
  
3.  変更するマッピングを含む行を選択し、[ **変更**] をクリックします。  
  
    [ **ターゲットスキーマの選択** ] ダイアログボックスで、使用可能なターゲットデータベースとスキーマを参照するか、2つの部分表記 (データベーススキーマ) のテキストボックスにデータベースとスキーマ名を入力し、[ **OK**] をクリックします。  
  
4.  [ **スキーママッピング** ] タブでターゲットが変更されます。  
  
**マッピングのモード**  
  
-   SQL Server へのマッピング  
  
ソースデータベースを任意のターゲットデータベースにマップできます。 既定では、ソースデータベースは SSMA を使用して接続したターゲットデータベースにマップされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 マップされているターゲットデータベースがに存在しない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"データベースまたはスキーマがターゲットメタデータに存在しません" というメッセージが表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。同期中に作成されます。続行しますか? "** [はい] をクリックします。 同様に、スキーマを、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同期中に作成されるターゲットデータベース下に存在しないスキーマにマップすることもできます。  
  
-   SQL Azure へのマッピング  
  
接続先データベースまたは接続先データベースの任意のスキーマに、ソースデータベースをマップでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 送信元スキーマを [接続されたターゲットデータベース] の既存ではないスキーマにマップすると、 **"スキーマはターゲットメタデータに存在しません" というメッセージが表示されます。同期中に作成されます。続行しますか?[はい] をクリックし** ます。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>既定のデータベースとスキーマに戻す  
MySQL スキーマと SQL Server スキーマ間のマッピングをカスタマイズする場合は、マッピングを既定値に戻すことができます。  
  
**既定のデータベースとスキーマに戻すには**  
  
1.  [スキーママッピング] タブで、任意の行を選択し、[既定 **値にリセット** ] をクリックして既定のデータベースとスキーマに戻します。  
  
## <a name="next-steps"></a>次の手順  
MySQL オブジェクトから SQL Server または SQL Azure オブジェクトへの変換を分析する場合は、 [変換レポートを作成](assessing-mysql-databases-for-conversion-mysqltosql.md) できます。そうしないと、 [mysql データベースオブジェクト定義](converting-mysql-databases-mysqltosql.md) を SQL Server または SQL Azure スキーマに変換できます。  
  
## <a name="see-also"></a>参照  
[プロジェクト設定 &#40;変換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Azure SQL Database &#40;MySQLToSQL&#41;に接続しています ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[MySQL データベースを SQL Server Azure SQL Database &#40;MySQLToSql&#41;に移行する ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[SQL Server &#40;MySQLToSQL&#41;に接続しています ](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
