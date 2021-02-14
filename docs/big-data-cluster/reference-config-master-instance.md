---
title: SQL Server マスター インスタンスの構成プロパティ
titleSuffix: SQL Server big data clusters
description: SQL Server マスター インスタンスのプロパティを構成するための参照記事。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f251357c818577b0ecd761c4a5ca2f030eeca58
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100043982"
---
# <a name="sql-server-master-instance-configuration-properties"></a>SQL Server マスター インスタンスの構成プロパティ

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

## <a name="properties"></a>プロパティ

展開時、マスター インスタンスに次の SQL Server オプションを構成できます。

|プロパティ|オプション|
| --- | --- |
|`[sqlagent]`|`enabled = { true | false }` |
|`[telemetry]`|`customerfeedback = { true | false }` |
|`[telemetry]`|`userRequestedLocalAuditDirectory = </path/file>`|
|`[licensing]`| `pid = { Enterprise | Developer }`|
|`[traceflag]`|` traceflag<#> = <####>`|

### <a name="examples"></a>例

次の例では、SQL エージェント、テレメトリを有効にし、Enterprise Edition の PID を設定し、トレース フラグ 1204 を有効にします。

```
[sqlagent]
enabled=true

[telemetry]
customerfeedback=true
userRequestedLocalAuditDirectory = /tmp/audit

[licensing]
pid = Enterprise

[traceflag]
traceflag0 = 1204
```

方法については、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] のマスター インスタンスを構成する](configure-sql-server-master-instance.md)方法に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] のマスター インスタンスを構成する](configure-sql-server-master-instance.md)
