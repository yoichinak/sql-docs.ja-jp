---
description: DROP ASSEMBLY (Transact-SQL)
title: DROP ASSEMBLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ASSEMBLY
- DROP_ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- deleting assemblies
- assemblies [CLR integration], removing
- dropping assemblies
- WITH NO DEPENDENTS option
ms.assetid: 452d181a-a8e6-44a3-975d-29966d01b18d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 601d7bdff19c6e6d8f4daec58c28c048891bcc82
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96131335"
---
# <a name="drop-assembly-transact-sql"></a>DROP ASSEMBLY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースから、アセンブリとそれに関連するすべてのファイルを削除します。 アセンブリは [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md) を使って作成し、[ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md) を使って変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
DROP ASSEMBLY [ IF EXISTS ] assembly_name [ ,...n ]  
[ WITH NO DEPENDENTS ]  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *IF EXISTS*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
 条件付きでは既に存在する場合にのみ、アセンブリを削除します。  
  
 *assembly_name*  
 削除するアセンブリの名前です。  
  
 WITH NO DEPENDENTS  
 指定した場合、*assembly_name* だけが削除され、アセンブリで参照される依存アセンブリは削除されません。 指定しない場合、DROP ASSEMBLY では *assembly_name* とすべての依存アセンブリが削除されます。  
  
## <a name="remarks"></a>解説  
 アセンブリを削除すると、データベースからアセンブリと、ソース コードやデバッグ ファイルなどのアセンブリに関連するファイルが削除されます。  
  
 WITH NO DEPENDENTS を指定しない場合、DROP ASSEMBLY では *assembly_name* とすべての依存アセンブリが削除されます。 依存アセンブリの削除に失敗した場合、DROP ASSEMBLY ではエラーが返されます。  
  
 アセンブリが、データベースに存在する他のアセンブリによって参照されているか、現在のデータベースの共通言語ランタイム (CLR) 関数、プロシージャ、トリガー、ユーザー定義型、または集計で使用されている場合、DROP ASSEMBLY ではエラーが返されます。  
  
 DROP ASSEMBLY は、アセンブリを参照する現在実行中のコードには影響を与えません。 ただし、DROP ASSEMBLY を実行した後では、アセンブリ コードの呼び出しは失敗します。  
  
## <a name="permissions"></a>アクセス許可  
 アセンブリの所有権、またはアセンブリに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、アセンブリ `HelloWorld` が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに既に作成されていることを前提としています。  
  
```sql  
DROP ASSEMBLY Helloworld ;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [アセンブリについての情報の取得](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
