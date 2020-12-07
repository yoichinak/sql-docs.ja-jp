---
description: dbo.sysschedules (Transact-SQL)
title: dbo.sysのスケジュール (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysschedules_TSQL
- sysschedules
- sysschedules_TSQL
- dbo.sysschedules
dev_langs:
- TSQL
helpviewer_keywords:
- sysschedules system table
ms.assetid: 4cac9237-7a69-4035-bb3e-928b76aad698
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9c0bb164d77ba4c505207e56897ecc17f8644821
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545813"
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ スケジュールに関する情報を格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントジョブスケジュールの ID。|  
|**schedule_uid**|**uniqueidentifier**|ジョブスケジュールの一意識別子。 この値は、分散ジョブのスケジュールを識別するために使用されます。|  
|**originating_server_id**|**int**|ジョブ スケジュールを取得したマスター サーバーの ID。|  
|**name**|**sysname (nvarchar (128))**|ジョブスケジュールのユーザー定義名。 この名前は、ジョブ内で一意である必要があります。|  
|**owner_sid**|**varbinary(85)**|Microsoft Windows *security_identifier* 、ジョブスケジュールを所有するユーザーまたはグループのものです。|  
|**有効**|**int**|ジョブスケジュールの状態:<br /><br /> **0** = 有効ではありません。<br /><br /> **1** = 有効。<br /><br /> スケジュールが有効になっていない場合、スケジュールに基づいてジョブは実行されません。|  
|**freq_type**|**int**|このスケジュールでジョブを実行する頻度。<br /><br /> **1** = 1 回のみ<br /><br /> **4** = 日単位<br /><br /> **8** = 週単位<br /><br /> **16** = 月単位<br /><br /> **32** = 毎月、 **freq_interval**に対して相対的<br /><br /> **64** = SQL Server エージェントサービスの開始時に実行されます<br /><br /> **128** = コンピューターがアイドル状態のときに実行|  
|**freq_interval**|**int**|ジョブが実行された日。 **Freq_type**の値によって異なります。 既定値は **0**で、 **freq_interval** が使用されていないことを示します。 有効な値とその影響については、次の表を参照してください。|  
|**freq_subday_type**|**int**|**Freq_subday_interval**の単位です。 使用可能な値とその説明を次に示します。<br /><br /> <br /><br /> **1** : 指定した時間に実行されます。<br /><br /> **2** : 秒<br /><br /> **4** : 分<br /><br /> **8** : 時間|  
|**freq_subday_interval**|**int**|ジョブの各実行間に発生する **freq_subday_type** 期間の数。|  
|**freq_relative_interval**|**int**|各月に **freq_interval** が発生した場合、 **freq_type** が **32** (月単位) になります。 次の値のいずれかです。<br /><br /> **0**  = **freq_relative_interval**が使用されていません<br /><br /> **1** = 最初<br /><br /> **2** = 秒<br /><br /> **4** = 3 番目<br /><br /> **8** = 4 番目<br /><br /> **16** = 最後|  
|**freq_recurrence_**<br /><br /> **段階**|**int**|ジョブのスケジュールされた実行の間隔を週または月単位で指定します。 **freq_recurrence_factor** は **freq_type** が **8**、 **16**、または **32**の場合にのみ使用されます。 この列に **0**が含まれている場合、 **freq_recurrence_factor** は使用されません。|  
|**active_start_date**|**int**|ジョブの実行を開始できる日付。 日付の形式は YYYYMMDD です。 NULL は今日の日付を示します。|  
|**active_end_date**|**int**|ジョブの実行を停止できる日付。 日付の形式は YYYYMMDD です。|  
|**active_start_time**|**int**|**Active_start_date**から、ジョブが実行を開始する**active_end_date**までの任意の日。 時刻の形式は HHMMSS で、24時間制を使用します。|  
|**active_end_time**|**int**|**Active_start_date**と、ジョブが実行を停止する**active_end_date**の間の任意の日。 時刻の形式は HHMMSS で、24時間制を使用します。|  
|**date_created**|**datetime**|スケジュールが作成された日付と時刻。|  
|**date_modified**|**datetime**|スケジュールが最後に変更された日付と時刻。|  
|**version_number**|**int**|スケジュールの現在のバージョン番号。 たとえば、スケジュールが10回変更された場合、 **version_number** は10になります。|  
  
|Freq_type の値|freq_interval への影響|  
|-------------------------|------------------------------|  
|**1** (1 回)|**freq_interval** が使用されていません (**0**)|  
|**4** (毎日)|**Freq_interval**日ごと|  
|**8** (毎週)|**freq_interval** は、次の1つまたは複数です。<br /><br /> **1** = 日曜日<br /><br /> **2** = 月曜日<br /><br /> **4** = 火曜日<br /><br /> **8** = 水曜日<br /><br /> **16** = 木曜日<br /><br /> **32** = 金曜日<br /><br /> **64** = 土曜日|  
|**16** (毎月)|月の **freq_interval** 日|  
|**32** (毎月、相対)|**freq_interval** は次のいずれかです。<br /><br /> **1** = 日曜日<br /><br /> **2** = 月曜日<br /><br /> **3** = 火曜日<br /><br /> **4** = 水曜日<br /><br /> **5** = 木曜日<br /><br /> **6** = 金曜日<br /><br /> **7** = 土曜日<br /><br /> **8** = 日<br /><br /> **9** = 平日<br /><br /> **10** = 週末|  
|**64** (SQL Server エージェントサービスの開始時に開始)|**freq_interval** が使用されていません (**0**)|  
|**128** (コンピューターがアイドル状態のときに実行されます)|**freq_interval** が使用されていません (**0**)|  
  
## <a name="see-also"></a>関連項目  
 [dbo.sysjobschedules &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
