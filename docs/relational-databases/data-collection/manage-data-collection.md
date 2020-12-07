---
description: データ コレクションの管理
title: データ コレクションの管理 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
keywords:
- データ収集
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 754aff825e0da8fd888deafb927936599a4d8631
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196766"
---
# <a name="manage-data-collection"></a>データ コレクションの管理
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] のストアド プロシージャと関数を使用して、データ コレクションの有効化または無効化、コレクション セットの構成の変更、管理データ ウェアハウスのデータの表示など、データ コレクションのさまざまな側面を管理します。  
  
## <a name="manage-data-collection-using-ssms"></a>SSMS を使用したデータ コレクションの管理  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のオブジェクト エクスプローラーを使用することで、次のデータ コレクター関連のタスクを実行します。  
  
-   [管理データ ウェアハウスの構成 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [データ コレクターのプロパティの構成](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)  
  
-   [データ コレクションを有効または無効にする方法](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [コレクション セットの開始または停止](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [SQL Server Profiler を使用して SQL トレース コレクション セットを作成する &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [コレクション セット ログの表示 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-collection-set-logs-sql-server-management-studio.md)  
  
-   [コレクション セットのスケジュールの表示または変更 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [コレクション セット レポートの表示 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-using-transact-sql"></a>Transact-SQL を使用したデータ コレクションの管理  
 データ コレクターにはストアド プロシージャの豊富なコレクションがあり、それらを使用してデータ コレクターの関連タスクを実行することができます。 たとえば、 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用すると、次のタスクを実行できます。  
  
-   [データ コレクションのパラメーターの構成 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md)  
  
-   [データ コレクションを有効または無効にする方法](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [コレクション セットの開始または停止](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [ジェネリック T-SQL Query コレクター型を使用するカスタム コレクション セットの作成 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [コレクション アイテムをコレクション セットに追加する &#40;Transact-SQL&#41;](../../relational-databases/data-collection/add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 さらに、msdb および管理データ ウェアハウスのデータベースの構成データ、実行ログ データ、および管理データ ウェアハウスに格納されているデータの取得に使用できる関数やビューもあります。  
  
 用意されているストアド プロシージャ、関数、およびビューを使用して、独自のエンド ツー エンドのデータ コレクション シナリオを作成することもできます。  
  
>**重要!!** 通常のストアド プロシージャとは異なり、データ コレクターで使用するストアド プロシージャではパラメーターのデータ型が厳密に定義されており、データ型の自動変換はサポートされていません。 これらのパラメーターが、引数の説明で指定されている正しいデータ型で呼び出されないと、このストアド プロシージャではエラーが返されます。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、付属のコード サンプルを作成して実行します。 詳細については、「 [オブジェクト エクスプローラー](../../ssms/object/object-explorer.md)」を参照してください。 また、任意のエディターでクエリを作成し、.sql というファイル名拡張子を持つテキスト ファイルに保存することもできます。 このクエリは、Windows コマンド プロンプトから **sqlcmd** ユーティリティを使用して実行できます。 詳細については、「 [sqlcmd Utility の使用](../../ssms/scripting/sqlcmd-use-the-utility.md)」を参照してください。  
  
### <a name="stored-procedures-and-views"></a>ストアド プロシージャとビュー  
 **データ コレクターの操作**  
  
 次の表に、データ コレクターの操作に使用できるストアド プロシージャを示します。  
  
|プロシージャ名|説明|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)|データ コレクターを有効にします。|  
|[sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)|データ コレクターを無効にします。|  
  
 **コレクション セットの操作**  
  
 次の表に、コレクション セットの操作に使用できるストアド プロシージャを示します。  
  
|プロシージャ名|説明|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)|コレクション セットを要求時に実行します。|  
|[sp_syscollector_start_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md)|コレクション セットを開始します。|  
|[sp_syscollector_stop_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)|コレクション セットを停止します。|  
|[sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)|コレクション セットを作成します。|  
|[sp_syscollector_delete_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql.md)|コレクション セットを削除します。|  
|[sp_syscollector_update_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql.md)|コレクション セットの構成を変更します。|  
|[sp_syscollector_update_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql.md)|コレクション セットのデータを管理データ ウェアハウスにアップロードします。 これは、実質的にはオンデマンドのアップロードです。|  
  
 **コレクション アイテムの操作**  
  
 次の表に、コレクション アイテムの操作に使用できるストアド プロシージャを示します。  
  
|プロシージャ名|説明|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)|コレクション アイテムを作成します。|  
|[sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)|コレクション アイテムを削除します。|  
|[sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)|コレクション アイテムを更新します。|  
  
 **コレクター型の操作**  
  
 次の表に、コレクター型の操作に使用できるストアド プロシージャを示します。  
  
|プロシージャ名|説明|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql.md)|コレクター型を作成します。|  
|[sp_syscollector_update_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql.md)|コレクター型を更新します。|  
|[sp_syscollector_delete_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql.md)|コレクター型を削除します。|  
  
 **構成情報の取得**  
  
 次の表に、構成情報や実行ログ データの取得に使用できるビューを示します。  
  
|ビューの名前|説明|  
|---------------|-----------------|  
|[syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|データ コレクターの構成を取得します。|  
|[syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|コレクション アイテムの情報を取得します。|  
|[syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|コレクション セットの情報を取得します。|  
|[syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|コレクター型の情報を取得します。|  
|[syscollector_execution_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|コレクション セットとパッケージの実行に関する情報を取得します。|  
|[syscollector_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)|タスクの実行に関する情報を取得します。|  
|[syscollector_execution_log_full &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|実行ログがいっぱいになったときに情報を取得します。|  
  
 **管理データ ウェアハウスへのアクセスの構成**  
  
 次の表に、管理データ ウェアハウスへのアクセスの構成に使用できるストアド プロシージャを示します。  
  
|プロシージャ名|説明|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)|管理データ ウェアハウスの接続文字列で定義されているデータベース名を指定します。|  
|[sp_syscollector_set_warehouse_instance_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)|管理データ ウェアハウスの接続文字列で定義されているインスタンスを指定します。|  
  
 **管理データ ウェアハウスの構成**  
  
 次の表に、管理データ ウェアハウスの構成の操作に使用できるストアド プロシージャを示します。  
  
|プロシージャ名|説明|  
|--------------------|-----------------|  
|[core.sp_create_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql.md)|管理データ ウェアハウス内にコレクションのスナップショットを作成します。|  
|[core.sp_update_data_source &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql.md)|データ コレクションのデータ ソースを更新します。|  
|[core.sp_add_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql.md)|管理データ ウェアハウスにコレクター型を追加します。|  
|[core.sp_remove_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql.md)|管理データ ウェアハウスからコレクター型を削除します。|  
|[core.sp_purge_data &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql.md)|管理データ ウェアハウスからデータを削除します。|  
  
 **アップロード パッケージの操作**  
  
 次の表に、アップロード パッケージの操作に使用できるストアド プロシージャを示します。  
  
|プロシージャ名|説明|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)|データのアップロードの再試行回数を構成します。|  
|[sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)|アップロードを次に再試行するまでのデータの一時ストレージを指定します。|  
  
 **データ コレクションの実行ログの操作**  
  
 次の表に、データ コレクションの実行ログの操作に使用できるストアド プロシージャを示します。  
  
|プロシージャ名|説明|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql.md)|実行ログからコレクション セットのエントリを削除します。|  
  
### <a name="functions"></a>関数  
 次の表に、実行情報とトレース情報の取得に使用できる関数を示します。  
  
|関数名|説明|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md)|特定のパッケージに関する [!INCLUDE[ssIS](../../includes/ssis-md.md)] の実行ログ データを取得します。|  
|[fn_syscollector_get_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql.md)|コレクション セットまたはパッケージの実行統計を取得します。 この情報には、ログに記録されたエラーが含まれます。|  
|[snapshots.fn_trace_getdata &#40;Transact-SQL&#41;](../../relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql.md)|ジェネリック SQL トレース コレクター型を使用したデータ収集時にログに記録されたイベントを取得します。|  
  
## <a name="see-also"></a>関連項目  
 [ストアド プロシージャの実行](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)   
 [SQL Server Management Studio の使用 [SQL Server]](../../ssms/sql-server-management-studio-ssms.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
