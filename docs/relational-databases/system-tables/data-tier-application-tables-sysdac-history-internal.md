---
description: データ層アプリケーション テーブル - sysdac_history_internal
title: sysdac_history_internal (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_history_internal
- sysdac_history_internal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_history_internal
ms.assetid: 774a1678-0b27-42be-8adc-a6d7a4a56510
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7f89db526d638a6e934e8db7ac791875b467e487
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544647"
---
# <a name="data-tier-application-tables---sysdac_history_internal"></a>データ層アプリケーション テーブル - sysdac_history_internal
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データ層アプリケーション (DAC) を管理するために実行したアクションについての情報を格納します。 このテーブルは、 **msdb**データベースの**dbo**スキーマに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**action_id**|**int**|アクションの識別子。|  
|**sequence_id**|**int**|アクション内のステップを識別します。|  
|**instance_id**|**uniqueidentifier**|DAC インスタンスの識別子。 この列は、 [transact-sql&#41;&#40;dac_instancesdbo.sys](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)の**instance_id**列に結合できます。|  
|**action_type**|**tinyint**|アクションの種類の識別子。<br /><br /> **0** = 配置<br /><br /> **1** = 作成<br /><br /> **2** = 名前の変更<br /><br /> **3** = デタッチ<br /><br /> **4** = 削除|  
|**action_type_name**|**varchar (19)**|アクションの種類の名前:<br /><br /> **deploy**<br /><br /> **create**<br /><br /> **rename**<br /><br /> **分離**<br /><br /> **delete**|  
|**dac_object_type**|**tinyint**|アクションの影響を受けるオブジェクトの種類の識別子。<br /><br /> **0** = dacpac<br /><br /> **1** = ログイン<br /><br /> **2** = データベース|  
|**dac_object_type_name**|**varchar (8)**|アクションによって影響を受けるオブジェクトの種類の名前。<br /><br /> **dacpac** = DAC インスタンス<br /><br /> **ログイン**<br /><br /> **database**|  
|**action_status**|**tinyint**|アクションの現在のステータスを識別するコード。<br /><br /> **0** = 保留中<br /><br /> **1** = 成功<br /><br /> **2** = 失敗|  
|**action_status_name**|**varchar (11)**|アクションの現在のステータス。<br /><br /> **pending**<br /><br /> **ブランド**<br /><br /> **オーバー**|  
|**必須**|**bit**|DAC 操作をロールバックするときに、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって使用されます。|  
|**dac_object_name_pretran**|**sysname**|アクションを含むトランザクションがコミットされる前のオブジェクトの名前。 データベースおよびログインにのみ使用されます。|  
|**dac_object_name_posttran**|**sysname**|アクションを含んでいるトランザクションをコミットした後のオブジェクトの名前。 データベースおよびログインにのみ使用されます。|  
|**sqlscript**|**nvarchar(max)**|データベースまたはログイン上でアクションを実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト。|  
|**ペイ**|**varbinary(max)**|バイナリエンコードされた文字列に保存された DAC パッケージ定義。|  
|**コメント**|**varchar(max)**|DAC のアップグレードでデータ損失の可能性を受け入れたユーザーのログインを記録します。|  
|**error_string**|**nvarchar(max)**|アクションでエラーが発生した場合に生成されるエラーメッセージ。|  
|**created_by**|**sysname**|このエントリを作成したアクションを開始したログイン。|  
|**date_created**|**datetime**|このエントリが作成された日付と時刻。|  
|**date_modified**|**datetime**|エントリが最後に変更された日付と時刻。|  
  
## <a name="remarks"></a>解説  
 Dac の配置や削除などの DAC 管理操作では、複数の手順が生成されます。 各アクションには、アクション識別子が割り当てられます。 各ステップには、シーケンス番号と **sysdac_history_internal**内の行が割り当てられます。この場合、ステップの状態が記録されます。 各行は、アクションステップの開始時に作成され、操作の状態を反映するために必要に応じて更新されます。 たとえば、[DAC の配置] アクションを 12 **action_id** 割り当て、 **sysdac_history_internal**の4つの行を取得することができます。  
  
| action_id | sequence_id | action_type_name | dac_object_type_name |
| --------- | ----------- | ---------------- | -------------------- |
|12|0|create|.dacpac|  
|12|1|create|ログイン (login)|  
|12|2|create|database|  
|12|3|rename|database|  
  
 Delete などの DAC 操作では、 **sysdac_history_internal**から行が削除されません。 次のクエリを使用すると、のインスタンスに配置されなくなった Dac の行を手動で削除でき [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。  
  
```sql  
DELETE FROM msdb.dbo.sysdac_history_internal  
WHERE instance_id NOT IN  
   (SELECT instance_id  
    FROM msdb.dbo.sysdac_instances_internal);  
```  
  
 アクティブな Dac の行を削除しても、DAC 操作には影響しません。唯一の影響は、DAC の完全な履歴を報告できないことです。  
  
> [!NOTE]  
>  現時点では、 **sysdac_history_internal** 行を削除するためのメカニズムはありません [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールのメンバーシップが必要です。 このビューへの読み取り専用アクセスは、master データベースに接続する権限を持つすべてのユーザーが使用できます。  
  
## <a name="see-also"></a>参照  
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)   
 [sysdac_instances_internal &#40;Transact-sql&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-instances-internal.md)  
  
  
