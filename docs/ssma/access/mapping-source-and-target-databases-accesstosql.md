---
title: ソースデータベースとターゲットデータベースのマッピング (Sql server の場合) |Microsoft Docs
description: 複数のデータベースに対して複数のデータベースを含め、SQL Server または Azure SQL Database へのアクセスデータベースの移行先となるデータベースを指定する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 966ec1472737f0e4d67615d4e7eb65df01a52cf4
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100059053"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>ソースデータベースとターゲットデータベースのマッピング (Sql server)
または SQL Azure に接続する場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、移行するターゲットデータベースを指定する必要があります。 複数の Access データベースがある場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、複数のデータベース (またはスキーマ)、または接続された Azure SQL Database の複数のスキーマにマップできます。  
  
## <a name="sql-server-or-azure-sql-database-schemas"></a>スキーマの SQL Server または Azure SQL Database  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースでは、スキーマの概念を使用して、データベース内のオブジェクトを論理グループに分割します。 たとえば、ライブラリデータベースでは、 **books**、 **audio**、video という3つのスキーマを使用して、書籍、オーディオ、およびビデオオブジェクトを相互に **分離すること** ができます。 既定では、access データベースは、の **master** データベースおよび **dbo** スキーマに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure の接続されたデータベースおよび **dbo** スキーマにマップされます。  
  
各 Access データベースとデータベースおよびスキーマ間のマッピングをカスタマイズしない限り [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA は、access データベースに関連付けられているすべてのスキーマとデータを、マップされた既定のデータベースに移行します。  
  
## <a name="modifying-the-target-database-and-schema"></a>ターゲットデータベースとスキーマの変更  
SSMA を使用すると、各 Access データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database にマップできます。 次の手順では、データベースごとにマッピングをカスタマイズする方法について説明します。  
  
**ターゲットデータベースとスキーマを変更するには**  
  
1.  [メタデータエクスプローラーにアクセス] ウィンドウで、[ **アクセス-メタデータ**] を選択します。  
  
    スキーママッピングは、[ **データベース** ] ノードまたは任意のデータベースノードを選択した場合にも使用できます。 [スキーママッピング] の一覧は、選択したオブジェクトに合わせてカスタマイズされています。  
  
2.  右ペインで、[ **スキーママッピング** ] タブをクリックします。  
  
    Access データベース名とそれに対応する ssNoVersion または Sql Azure スキーマを含むテーブルが表示されます。 ターゲットスキーマは、2つの部分表記 (データベーススキーマ) で示されます。  
  
3.  カスタマイズするマッピングが含まれている行を選択し、[ **変更**] をクリックします。  
  
4.  [ **ターゲットスキーマの選択** ] ダイアログボックスで、使用可能なターゲットデータベースとスキーマを参照するか、2つの部分表記 (データベーススキーマ) のテキストボックスにデータベースとスキーマ名を入力し、[ **OK**] をクリックします。  
  
**マッピングのモード**  
  
-   SQL Server へのマッピング  
  
ソースデータベースを任意のターゲットデータベースにマップできます。 既定では、ソースデータベースは SSMA を使用して接続したターゲットデータベースにマップされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 マップされているターゲットデータベースがに存在しない場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **"データベースまたはスキーマがターゲットメタデータに存在しません" というメッセージが表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。同期中に作成されます。続行しますか? "** [はい] をクリックします。 同様に、スキーマを、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同期中に作成されるターゲットデータベース下に存在しないスキーマにマップすることもできます。  
  
-   SQL Azure へのマッピング  
  
接続先データベースまたは接続先データベースの任意のスキーマに、ソースデータベースをマップでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 送信元スキーマを [接続されたターゲットデータベース] の既存ではないスキーマにマップすると、 **"スキーマはターゲットメタデータに存在しません" というメッセージが表示されます。同期中に作成されます。続行しますか?[はい] をクリックし** ます。  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>最初のデータベースとスキーマに戻す  
Access データベースとまたはの Azure SQL Database 間のマッピングをカスタマイズする場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続時に指定したデータベース、または SQL Azure にマッピングを戻すことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**既定のデータベースとスキーマにリセットするには**  
  
1.  [スキーママッピング] タブで、任意の行を選択し、[既定 **値にリセット** ] をクリックして既定のデータベースとスキーマに戻します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順では、[データベースオブジェクトを変換](converting-access-database-objects-accesstosql.md)します。  
  
## <a name="see-also"></a>参照  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
