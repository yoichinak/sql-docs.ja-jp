---
description: sysssislog (Transact-sql)
title: sysssislog (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 58ce8d5a4784f34e83e2b09edda63dd49833a5ab
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99159474"
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パッケージ、または実行時にタスクとコンテナーによって生成されるログエントリごとに1行のレコードを格納します。 このテーブルは、のインストール時に msdb データベースに作成され [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ます。 ログ記録が別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに記録されるように構成する場合、ここで説明する形式の sysssislog テーブルが、指定されたデータベースに作成されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージがログプロバイダーを使用する場合に **のみ** 、このテーブルにログエントリを書き込みます [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**int**|ログエントリの一意の識別子。|  
|イベント|**sysname**|ログ エントリを生成したイベントの名前。|  
|コンピュータ|**nvarchar**|ログ エントリの生成時にパッケージが実行されていたコンピューター。|  
|operator|**nvarchar**|ログエントリを生成したパッケージを実行したユーザーのユーザー名。|  
|source|**nvarchar**|ログエントリを生成した、パッケージ内の実行可能ファイルの名前。|  
|sourceid|**uniqueidentifier**|ログ エントリを生成したパッケージ内の実行可能ファイルの GUID。|  
|executionid|**uniqueidentifier**|ログエントリを生成した実行可能ファイルの実行インスタンスの GUID。|  
|starttime|**datetime**|パッケージの実行が開始された時刻です。|  
|endtime|**datetime**|パッケージが完了した時刻です。<br /><br /> この機能は実装されていません。 Endtime 列の値は、常に starttime 列の値と同じです。|  
|datacode|**int**|コンテナーまたはタスクの実行結果を示す省略可能な整数値。|  
|databytes|**image**|追加情報を格納しているバイト配列 (省略可能)。|  
|message|**nvarchar**|イベントの説明とイベントに関連付けられている情報。|  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
