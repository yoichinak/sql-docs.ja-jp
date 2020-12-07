---
description: DB2 スキーマを SQL Server スキーマ (DB2ToSQL) にマッピングする
title: DB2 スキーマを SQL Server スキーマ (DB2ToSQL) にマッピングするMicrosoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9942d2ee78932c3bb8bed2baac0885b68e40049d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869567"
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>DB2 スキーマを SQL Server スキーマ (DB2ToSQL) にマッピングする
DB2 では、各データベースに1つ以上のスキーマがあります。 既定では、SSMA は、DB2 スキーマ内のすべてのオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、スキーマのという名前のデータベースに移行します。 ただし、DB2 スキーマとデータベース間のマッピングをカスタマイズすることはでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 および SQL Server スキーマ  
DB2 データベースにはスキーマが含まれています。 のインスタンスには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複数のデータベースが含まれており、それぞれが複数のスキーマを持つことができます。  
  
DB2 のスキーマの概念は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの概念とそのスキーマの1つにマップされます。 たとえば、DB2 に **HR** という名前のスキーマがあるとします。 のインスタンスには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **HR** という名前のデータベースがあり、そのデータベース内にはスキーマがあります。 1つのスキーマは、 **dbo** (またはデータベース所有者) スキーマです。 既定では、DB2 スキーマの **hr** は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースとスキーマの **hr. dbo** にマップされます。 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とは、スキーマとしてのデータベースとスキーマの組み合わせを意味します。  
  
DB2 とスキーマ間のマッピングを変更でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="modifying-the-target-database-and-schema"></a>ターゲットデータベースとスキーマの変更  
SSMA では、使用可能な任意のスキーマに DB2 スキーマをマップでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**データベースとスキーマを変更するには**  
  
1.  DB2 メタデータエクスプローラーで、[ **スキーマ**] を選択します。  
  
    [ **スキーママッピング** ] タブは、個々のデータベース、 **スキーマ** フォルダー、または個々のスキーマを選択した場合にも使用できます。 [ **スキーママッピング** ] タブの一覧は、選択したオブジェクトに合わせてカスタマイズされています。  
  
2.  右ペインで、[ **スキーママッピング** ] タブをクリックします。  
  
    すべての DB2 スキーマの一覧が表示され、その後にターゲット値が表示されます。 このターゲットは、のオブジェクトとデータを移行する2つの部分表記 (*データベーススキーマ*) で示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ています。  
  
3.  変更するマッピングを含む行を選択し、[ **変更**] をクリックします。  
  
    [ **ターゲットスキーマの選択** ] ダイアログボックスで、使用可能なターゲットデータベースとスキーマを参照するか、2つの部分表記 (データベーススキーマ) のテキストボックスにデータベースとスキーマ名を入力し、[ **OK**] をクリックします。  
  
4.  [ **スキーママッピング** ] タブでターゲットが変更されます。  
  
**マッピングのモード**  
  
-   SQL Server へのマッピング  
  
ソースデータベースを任意のターゲットデータベースにマップできます。 既定では、ソースデータベースは SSMA を使用して接続したターゲットデータベースにマップされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 マップされているターゲットデータベースがに存在しない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"データベースまたはスキーマがターゲットメタデータに存在しません" というメッセージが表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。同期中に作成されます。続行しますか? "** [はい] をクリックします。 同様に、スキーマを、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同期中に作成されるターゲットデータベース下に存在しないスキーマにマップすることもできます。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>既定のデータベースとスキーマに戻す  
DB2 スキーマとスキーマ間のマッピングをカスタマイズする場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マッピングを既定値に戻すことができます。  
  
**既定のデータベースとスキーマに戻すには**  
  
1.  [スキーママッピング] タブで、任意の行を選択し、[既定 **値にリセット** ] をクリックして既定のデータベースとスキーマに戻します。  
  
## <a name="next-steps"></a>次の手順  
DB2 オブジェクトからオブジェクトへの変換を分析する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [データ移行レポート (Ssma Common)](../sybase/data-migration-report-sybasetosql.md)を使用できます。  
  
## <a name="see-also"></a>参照  
[SQL Server &#40;DB2ToSQL&#41;に接続しています ](../../ssma/db2/connecting-to-sql-server-db2tosql.md)  
[DB2 データベースを SQL Server &#40;DB2ToSQL&#41;に移行する ](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
