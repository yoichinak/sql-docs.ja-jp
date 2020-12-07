---
description: dm_os_cluster_properties (Transact-sql)
title: dm_os_cluster_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_properties_TSQL
- sys.dm_os_cluster_properties
- dm_os_cluster_properties_TSQL
- dm_os_cluster_properties
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_cluster_properties
- sys.dm_os_cluster_properties
ms.assetid: 6d82e770-fba7-49e0-9a0c-3b34b393e4a7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f90e54197387bf0bd64bf5c890ab3a044883bbd9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550248"
---
# <a name="sysdm_os_cluster_properties-transact-sql"></a>dm_os_cluster_properties (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このトピックで特定されたクラスターリソースプロパティの現在の設定を持つ1行を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このビューがのスタンドアロンインスタンスで実行されている場合、データは返されません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 これらのプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスのエラー検出、障害応答時間、および正常性状態の監視のログ記録に影響を与える値を設定するために使用されます。  
  

|列名|プロパティ|説明|  
|-----------------|--------------|-----------------|  
|VerboseLogging|bigint|SQL Server フェールオーバー クラスターのログ記録レベルです。 詳細ログをオンにすると、トラブルシューティングを目的とした詳細情報をエラー ログに追加できます。 次のいずれかの値です。<br /><br /> 0: ログ記録はオフです (既定)<br /><br /> 1: エラーのみ。<br /><br /> 2: エラーおよび警告<br /><br /> 詳細については、「 [ALTER SERVER CONFIGURATION &#40;transact-sql&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)」を参照してください。|  
|SqlDumperDumpFlags|bigint|ダンプフラグは、によって生成されるダンプファイルの種類を決定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 既定の設定は 0 です。|  
|SqlDumperDumpPath|nvarchar(260)|ダンプファイルを生成するためのユーティリティが格納されている場所。|  
|SqlDumperDumpTimeOut|bigint|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でエラーが発生した場合の、SQLDumper ユーティリティによるダンプの生成のタイムアウト値 (ミリ秒単位) です。 既定値は 0 です。|  
|FailureConditionLevel|bigint|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのエラーまたは再起動の条件を設定します。 既定値は、3 です。 詳細な説明やプロパティ設定の変更については、「 [FailureConditionLevel プロパティ設定の構成](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)」を参照してください。|  
|HealthCheckTimeout|bigint|SQL Server データベース エンジンのリソース DLL が、サーバーの状態情報を待機する時間のタイムアウト値です。この待機時間を経過すると、SQL Server のインスタンスが応答不能と見なされます。 このタイムアウト値は、ミリ秒単位で指定します。 既定値は6万です。 このプロパティ設定の詳細や変更については、「 [Configure HealthCheckTimeout Property Settings](../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)」を参照してください。|  
  
## <a name="permissions"></a>アクセス許可  
 フェールオーバークラスターインスタンスに対する VIEW SERVER STATE 権限が必要です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="examples"></a>例  
 次の例では、sys.dm_os_cluster_properties を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター リソースのプロパティ設定を返します。  
  
```  
SELECT VerboseLogging, SqlDumperDumpFlags, SqlDumperDumpPath, SqlDumperDumpTimeOut, FailureConditionLevel, HealthCheckTimeout  
FROM sys.dm_os_cluster_properties;  
```  
  
 次に結果セットの例を示します。  
  
|VerboseLogging|SqlDumperDumpFlags|SqlDumperDumpPath|SqlDumperDumpTimeOut|FailureConditionLevel|HealthCheckTimeout|  
|--------------------|------------------------|-----------------------|--------------------------|---------------------------|------------------------|  
|0|0|NULL|0|3|60000|  
  
  
