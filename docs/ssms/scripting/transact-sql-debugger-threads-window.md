---
title: '[スレッド] ウィンドウ'
description: '[スレッド] ウィンドウについて説明します。これには、デバッグ中のデータベース エンジン スレッドに関する情報が表示されます。 情報はデバッグ モードでのみ表示されます。'
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: da80bf7a847e6724eaad79d2efd86a0b095b6b52
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036146"
---
# <a name="transact-sql-debugger---threads-window"></a>Transact-SQL デバッガー - [スレッド] ウィンドウ

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**[スレッド]** ウィンドウには、デバッグ中の [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター セッションで使用されている [!INCLUDE[ssDE](../../includes/ssde-md.md)] スレッドに関する情報が表示されます。 スレッドの情報を表示するには、デバッグ モードである必要があります。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>タスク一覧

**[スレッド] ウィンドウにアクセスするには**
  
-   **[デバッグ]** メニューの **[ウィンドウ]** をポイントし、 **[スレッド]** をクリックします。  
  
## <a name="columns"></a>[列]  
 **ID**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーがスレッドに割り当てる一意な識別番号。 スレッドの詳細情報を参照するには、sys.dm_os_threads 動的管理ビューから行を選択します。  
  
 簡易プーリング モードで実行していない場合は、os_thread_id の値が **[ID]** 列の値に一致する行を選択します。 簡易プーリング モードで実行している場合は、fiber_context_address の値が **[ID]** 列の値に一致する行を選択します。  
  
 **名前**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] セッションの情報を **ComputerName/InstanceName [SPID]** の形式で表示します。  
  
 **[ComputerName]**  
 クエリ エディター セッションが接続している [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを実行しているコンピューターの名前。  
  
 **InstanceName**  
 クエリ エディター セッションが接続している [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスの名前。  
  
 **[SPID]**  
 このセッションを一意に識別する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセッション プロセス ID。 セッションの詳細情報を参照するには、spid 列と同じ値を持つ sys.sysprocesses ビューの行を選択します。  
  
 **場所**  
 デバッグ中のクエリ エディター セッションで使用されているスクリプト ファイルの名前を表示します。  
  
 **優先順位**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーはこの機能をサポートしていません。  
  
 **[中断]**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーはこの機能をサポートしていません。  
  
## <a name="see-also"></a>参照  
 [Transact-SQL デバッガー](./transact-sql-debugger.md)   
 [Transact-SQL デバッガー情報](./transact-sql-debugger-information.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)