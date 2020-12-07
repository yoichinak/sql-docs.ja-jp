---
title: Transact-SQL によるインメモリ OLTP のサポート | Microsoft Docs
description: インメモリ OLTP をサポートする構文オプションを含む Transact-SQL ステートメントについて説明します。 サポートされている機能に関するその他の参照へのリンクをご利用ください。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dda00961f4d8aa7a5b220e2794105adbac74793b
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868254"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>Transact-SQL によるインメモリ OLTP のサポート
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  インメモリ OLTP をサポートするために、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに構文オプションが追加されました。  
  
-   [ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) (**MEMORY_OPTIMIZED_DATA** を追加)  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md) (**MEMORY_OPTIMIZED_DATA** を追加)  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
-   [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)  
  
-   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
    ネイティブ コンパイル ストアド プロシージャでは、変数を **NOT NULL**として宣言できます。 通常のストアド プロシージャでは行えません。  
  
 SQL Server 2016 以降では、メモリ最適化テーブルの **AUTO_UPDATE_STATISTICS** を **ON** に設定することができます。 詳細については、「[sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)」を参照してください。  
  
 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md) ON はネイティブ コンパイル ストアド プロシージャに対してサポートされていません。  
  
 サポートされていない機能の詳細については、「[インメモリ OLTP でサポートされていない Transact-SQL の構造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)」を参照してください。  
  
 ネイティブ コンパイル ストアド プロシージャでサポートされている構造については、「 [ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md) 」および「 [ネイティブ コンパイル ストアド プロシージャ上でサポートされる構造](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)」 を参照してください。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [ネイティブ コンパイル ストアド プロシージャの移行に関する問題](./a-guide-to-query-processing-for-memory-optimized-tables.md)   
 [インメモリ OLTP に対してサポートされていない SQL Server の機能](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)   
 [ネイティブ コンパイル ストアド プロシージャ](./a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
