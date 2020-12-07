---
description: sys.dm_clr_appdomains (Transact-sql)
title: sys.dm_clr_appdomains (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7f1357535d22306f09f8378e8e71aef6801975ae
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834106"
---
# <a name="sysdm_clr_appdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバー内のアプリケーションドメインごとに1行の値を返します。 アプリケーションドメイン (**AppDomain**) は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] アプリケーションの分離の単位である共通言語ランタイム (CLR) の構成要素です。 このビューを使用すると、で実行されている CLR 統合オブジェクトを理解し、トラブルシューティングを行うことができ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 CLR 統合マネージド データベース オブジェクトにはいくつかの種類があります。 これらのオブジェクトに関する一般的な情報については、「 [共通言語ランタイム (CLR) 統合によるデータベースオブジェクトの構築](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)」を参照してください。 これらのオブジェクトが実行されるたびに、に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] よって、必要なコードを読み込んで実行できる **AppDomain** が作成されます。 **Appdomain**の分離レベルは、所有者ごとにデータベースごとに1つの**appdomain**です。 つまり、ユーザーが所有するすべての CLR オブジェクトは、常にデータベースごとに同じ **AppDomain** で実行されます (ユーザーが異なるデータベースに clr データベースオブジェクトを登録した場合、clr データベースオブジェクトは異なるアプリケーションドメインで実行されます)。 コードの実行が完了した後、 **AppDomain** は破棄されません。 代わりに、以降の実行に備えて、メモリ内にキャッシュされます。 これによってパフォーマンスも向上します。  
  
 詳細については、「 [アプリケーションドメイン](../../sql-server/what-s-new-in-sql-server-2016.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary (8)**|**AppDomain**のアドレス。 ユーザーが所有するすべての管理対象データベースオブジェクトは、常に同じ **AppDomain**に読み込まれます。 この列を使用して、 **sys.dm_clr_loaded_assemblies**でこの**AppDomain**に現在読み込まれているすべてのアセンブリを検索できます。|  
|**appdomain_id**|**int**|**AppDomain**の ID。 各 **AppDomain** には一意の ID があります。|  
|**appdomain_name**|**varchar (386)**|によって割り当てられた **AppDomain** の名前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**creation_time**|**datetime**|**AppDomain**が作成された時刻。 **AppDomains**はキャッシュされ、パフォーマンス向上のために再利用されるため、 **creation_time**は必ずしもコードが実行された時間とは限りません。|  
|**db_id**|**int**|この **AppDomain** が作成されたデータベースの ID。 2つの異なるデータベースに格納されているコードは、1つの **AppDomain**を共有できません。|  
|**user_id**|**int**|この **AppDomain**でオブジェクトを実行できるユーザーの ID。|  
|**state**|**nvarchar(128)**|**AppDomain**の現在の状態の記述子。 AppDomain は、作成から削除まで、さまざまな状態になることがあります。 詳細については、このトピックの「解説」を参照してください。|  
|**strong_refcount**|**int**|この **AppDomain**への強い参照の数。 これは、この **AppDomain**を使用している現在実行中のバッチの数を反映します。 このビューを実行すると、 **強力な refcount**が作成されることに注意してください。が現在実行されているコードがない場合でも、 **strong_refcount** の値は1になります。|  
|**weak_refcount**|**int**|この **AppDomain**への弱参照の数。 これは、 **AppDomain** 内のキャッシュされているオブジェクトの数を示します。 マネージデータベースオブジェクトを実行すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 後で再利用するために、によって **AppDomain** 内にキャッシュされます。 これによってパフォーマンスも向上します。|  
|**cost**|**int**|**AppDomain**のコスト。 コストが高いほど、この **AppDomain** がメモリ不足でアンロードされる可能性が高くなります。 通常、コストは、この **AppDomain**を再作成するために必要なメモリ量によって異なります。|  
|**value**|**int**|**AppDomain**の値。 値が小さいほど、この **AppDomain** がメモリ不足でアンロードされる可能性が高くなります。 通常、値は、この **AppDomain**を使用している接続またはバッチの数によって異なります。|  
|**total_processor_time_ms**|**bigint**|プロセスの開始後、現在のアプリケーション ドメインでの実行中にすべてのスレッドによって使用された、ミリ秒単位の合計プロセッサ時間です。 これは、 **System. MonitoringTotalProcessorTime**と同じです。|  
|**total_allocated_memory_kb**|**bigint**|アプリケーション ドメインの作成後、それによって行われたすべてのメモリ割り当ての、KB 単位の合計サイズです。収集されたメモリ量も差し引かれません。 これは、 **MonitoringTotalAllocatedMemorySize**に相当します。|  
|**survived_memory_kb**|**bigint**|最後の完全なブロッキングコレクションの後に残っていた、現在のアプリケーションドメインによって参照されていることがわかっているキロバイト数。 これは、 **MonitoringSurvivedMemorySize**に相当します。|  
  
## <a name="remarks"></a>注釈  
 **Dm_clr_appdomains と appdomain_address**の間には、一対一のリレーションシップが**あります。**  
  
 次の表に、使用可能な **状態** の値とその説明、およびそれらが **AppDomain** のライフサイクルで発生するタイミングを示します。 この情報を使用すると、 **appdomain** のライフサイクルに従い、Windows イベントログを解析することなく、疑わしいまたは繰り返しの **appdomain** インスタンスのアンロードを監視できます。  
  
## <a name="appdomain-initialization"></a>AppDomain の初期化  
  
|State|説明|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|**AppDomain**を作成しています。|  
  
## <a name="appdomain-usage"></a>AppDomain の使用状況  
  
|State|説明|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|ランタイム **AppDomain** は、複数のユーザーが使用できる状態になっています。|  
|E_APPDOMAIN_SINGLEUSER|DDL 操作で **AppDomain** を使用する準備ができました。 これらは E_APPDOMAIN_SHARED とは異なり、CLR 統合の実行に DDL 操作ではなく共有 AppDomain が使用されます。 このような AppDomains は、他の同時実行操作から分離されています。|  
|E_APPDOMAIN_DOOMED|**AppDomain**はアンロードされるようにスケジュールされていますが、現在実行中のスレッドがあります。|  
  
## <a name="appdomain-cleanup"></a>AppDomain のクリーンアップ  
  
|State|説明|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR が **AppDomain**をアンロードするように要求しました。通常は、マネージデータベースオブジェクトを含むアセンブリが変更または削除されたことが原因です。|  
|E_APPDOMAIN_UNLOADED|CLR によって **AppDomain**がアンロードされました。 これは、通常、 **Threadabort**、 **OutOfMemory**、またはユーザーコードでのハンドルされない例外によるエスカレーション手順の結果です。|  
|E_APPDOMAIN_ENQUEUE_DESTROY|**AppDomain**は CLR でアンロードされ、によって破棄されるように設定されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|E_APPDOMAIN_DESTROY|**AppDomain**はによって破棄されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|E_APPDOMAIN_ZOMBIE|**Appdomain**はによって破棄されていますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **appdomain**へのすべての参照がクリーンアップされているわけではありません。|  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例は、特定のアセンブリの **AppDomain** の詳細を表示する方法を示しています。  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 次の例は、特定の **AppDomain**内のすべてのアセンブリを表示する方法を示しています。  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>参照  
 [sys.dm_clr_loaded_assemblies &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [Transact-sql&#41;&#40;共通言語ランタイム関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
