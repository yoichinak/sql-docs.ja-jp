---
title: CLR データベースオブジェクトからのデータアクセス |Microsoft Docs
description: CLR ルーチンは、SQL Server の .NET Framework Data Provider (SqlClient とも呼ばれます) を使用して、CLR データベースオブジェクト内からデータにアクセスできます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
author: rothja
ms.author: jroth
ms.openlocfilehash: 606beeaf190dfb4eb24101242ba1a6f2212303fb
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810844"
---
# <a name="data-access-from-clr-database-objects"></a>CLR データベース オブジェクトからのデータ アクセス
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  共通言語ランタイム (CLR) ルーチンは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リモートインスタンスに格納されているデータだけでなく、実行されるのインスタンスに格納されているデータにも簡単にアクセスできます。 ルーチンからどのデータにアクセスできるかは、コードが実行されているユーザー コンテキストによって決まります。 の .NET Framework Data Provider [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ( **SqlClient**とも呼ばれます) を使用して、CLR データベースオブジェクト内からデータにアクセスします。 これは、開発者がマネージド クライアント アプリケーションや中間層アプリケーションから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データにアクセスする際に使用するプロバイダーと同じです。 このため、クライアントおよび中間層アプリケーションでは、ADO.NET と **SqlClient** に関する知識を活用できます。  
  
> [!NOTE]  
>  ユーザー定義型メソッドとユーザー定義関数では、既定ではデータ アクセスの実行が許可されていません。 ユーザー定義型 (UDT) メソッドまたはユーザー定義関数からの読み取り専用データアクセスを有効にするには、 **SqlMethodAttribute**または**sqlfunctionattribute** **のデータアクセスプロパティを** **dataaccesskind**に設定する必要があります。 UDT またはユーザー定義関数によるデータ変更操作は許可されません。この操作を実行しようとすると、実行時に例外がスローされます。  
  
 ここでは、CLR データベース オブジェクト内からデータにアクセスする際の機能や動作の具体的な違いについて説明します。 ADO.NET の機能の詳細については、.NET Framework SDK に付属の ADO.NET のドキュメントを参照してください。  
  
 次の表に、このセクションの各トピックの一覧を示します。  
  
 [コンテキスト接続](../../../relational-databases/clr-integration/data-access/context-connection.md)  
 SQL Server へのコンテキスト接続について説明します。  
  
 [接続の権限借用と資格情報](../../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
 接続の権限借用および接続の資格情報について説明します。  
  
 [ADO.NET に対する SQL Server インプロセス固有の拡張機能](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 インプロセス固有の **SqlPipe**、 **sqlcontext**、 **Sqltriggercontext**、および **SqlDataRecord** オブジェクトについて説明します。  
  
 [CLR 統合とトランザクション](../../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
 System.Transactions 名前空間で提供される新しいトランザクション フレームワークを ADO.NET および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 統合と統合する方法について説明します。  
  
 [CLR データベース オブジェクトからの XML シリアル化](/dotnet/standard/serialization/introducing-xml-serialization)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部で CLR データベース オブジェクトの XML シリアル化のシナリオを有効にする方法について説明します。  
  
