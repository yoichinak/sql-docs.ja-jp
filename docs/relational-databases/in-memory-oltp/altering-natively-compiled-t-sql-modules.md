---
title: ネイティブ コンパイル T-SQL モジュールの変更 | Microsoft Docs
description: SQL Server と Azure SQL Database でネイティブ コンパイル ストアド プロシージャとネイティブ コンパイル Transact-SQL モジュールに対して ALTER 操作を実行する方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b52fb0f4a7e0df54964d5e127570856e7baa8e56
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867394"
---
# <a name="altering-natively-compiled-t-sql-modules"></a>Altering Natively Compiled T-SQL Modules
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、`ALTER` ステートメントを使用して、ネイティブ コンパイル ストアド プロシージャおよびスカラー UDF やトリガーなどの他のネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールに対して、`ALTER` 操作を実行できます。  
  
ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールに対して `ALTER` を実行すると、モジュールは新しい定義を使用して再コンパイルされます。 再コンパイルの進行中、古いバージョンのモジュールは引き続き実行に使用できます。 コンパイルが完了すると、モジュールの実行は削除され、新しいバージョンのモジュールがインストールされます。 ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールを変更する場合、次のオプションを変更できます。  
  
-   パラメーター  
-   EXECUTE AS  
-   TRANSACTION ISOLATION LEVEL  
-   LANGUAGE  
-   DATEFIRST  
-   DATEFORMAT  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
> ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールは、非ネイティブ コンパイル モジュールに変換できません。 非ネイティブ コンパイル T-SQL モジュールは、ネイティブ コンパイル モジュールに変換できません。  
  
`ALTER PROCEDURE` の機能と構文の詳細については、「[ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)」を参照してください。  
  
ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールに対して [sp_recompile](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) を実行できます。これにより、モジュールは次の実行時に再コンパイルされます。  
  
## <a name="example"></a>例  
次の例では、メモリ最適化テーブル (T1) と、T1 のすべての列を選択するネイティブ コンパイル ストアド プロシージャ (usp_1) が作成されます。 その後、usp_1 は、`EXECUTE AS` 句を削除し、`LANGUAGE` を変更して、T1 からただ 1 つの列 (C1) を選択するように変更されます。  
  
```sql  
CREATE TABLE [dbo].[T1] (  
  [c1] [int] NOT NULL,  
  [c2] [float] NOT NULL,  
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
   SELECT c1, c2 FROM dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
   SELECT c1 FROM dbo.T1  
END  
GO    
```   
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](./a-guide-to-query-processing-for-memory-optimized-tables.md)