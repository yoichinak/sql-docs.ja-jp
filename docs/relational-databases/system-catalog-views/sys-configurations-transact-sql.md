---
description: sys.configurations (Transact-SQL)
title: sys.configurations (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6273f057b7733b787ed2ed8e8b61d23fd107fbd7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546839"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  システム内のサーバー全体の構成オプション値ごとに1行の値を格納します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|構成値の一意の ID。|  
|**name**|**nvarchar(35)**|構成オプションの名前。|  
|**value**|**sql_variant**|このオプションの値を構成しました。|  
|**minimum**|**sql_variant**|構成オプションの最小値。|  
|**maximum**|**sql_variant**|構成オプションの最大値。|  
|**value_in_use**|**sql_variant**|オプションで現在有効な実行値|  
|**description**|**nvarchar (255)**|構成オプションの説明|  
|**is_dynamic**|**bit**|1 = 再構成ステートメントが実行されたときに有効になる変数です。|  
|**is_advanced**|**bit**|1 = 変数は、 **show advancedoption** が設定されている場合にのみ表示されます。|  
  
 ## <a name="remarks"></a>解説
  すべてのサーバー構成オプションの一覧については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  データベースレベルの構成オプションについては、「 [ALTER DATABASE スコープ構成 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)」を参照してください。 ソフト NUMA を構成するには、「 [ソフト numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)」を参照してください。  
 
sys.configurations カタログビューを使用すると、config_value ([値] 列)、run_value (value_in_use 列)、および構成オプションが動的 (サーバーエンジンの再起動または is_dynamic 列) かどうかを判断できます。

> [!NOTE]
> Sp_configure の結果セットの config_value は、 **sys.configurations 値** 列と同じです。 **Run_value**は、 **sys.configurations value_in_use**列に相当します。

次のクエリを使用して、構成済みの値がインストールされていないかどうかを確認できます。

```SQL
select * from sys.configurations where value != value_in_use
```

値が構成オプションの変更と同じで、 **value_in_use** が同じでない場合は、再構成コマンドが実行されていないか、失敗したか、またはサーバーエンジンを再起動する必要があります。

値と value_in_use が同じではなく、これが想定される動作である構成オプションがあります。 次に例を示します。

"max server memory (MB)"-0 の既定の構成値は value_in_use = 2147483647 "min server memory (MB)" と表示されます。既定の構成値0は、value_in_use = 8 (32 ビット) または 16 (64 ビット) として表示される場合があります。 

場合によっては、 **value_in_use** が0になります。 この場合、"true" **value_in_use** は 8 (32 ビット) または 16 (64 ビット) です。

**Is_dynamic**列を使用して、構成オプションに再起動が必要かどうかを判断できます。 is_dynamic = 1 は、再構成 (t-sql) のコマンドが実行されると、新しい値が "直ちに" 有効になることを意味します (場合によっては、サーバーエンジンが新しい値をすぐに評価するのではなく、通常の実行時にその値が使用されます)。 is_dynamic = 0 の場合、変更された構成値は、再構成 (T-sql) コマンドが実行された場合でも、サーバーが再起動されるまで有効になりません。

動的でない構成オプションの場合、構成変更のインストールの最初の手順を実行するために再構成 (T-sql) コマンドが実行されているかどうかを確認する方法はありません。 SQL Server を再起動して構成の変更をインストールする前に、再構成 (T-sql) コマンドを実行して、SQL Server の再起動後にすべての構成変更が有効になるようにします。 
 
 
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サーバー全体の構成のカタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
