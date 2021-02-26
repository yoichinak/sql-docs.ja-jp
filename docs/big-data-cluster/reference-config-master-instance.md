---
title: SQL Server マスター インスタンスの構成プロパティ
titleSuffix: SQL Server big data clusters
description: SQL Server マスター インスタンスのプロパティを構成するための参照記事。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 02/11/2021
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2d986013374e7f69111288d2d0f50b09130a2d68
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100343508"
---
# <a name="sql-server-master-instance-configuration-properties----pre-cu9-release"></a>SQL Server マスター インスタンスの構成プロパティ - CU9 より前のリリース

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]
> [!NOTE]
> 次の情報は、構成が有効になっていない CU9 より前のリリース クラスターにのみ適用できます。また、SQL Server マスター インスタンスを構成するには、mssql-conf が必要です。 CU9 以降のリリース クラスターでは、構成管理機能を利用することができ、mssql conf ファイルが不要になりました。 SQL Server マスター インスタンスとその他の BDC コンポーネントで使用可能な構成については、[こちら](reference-config-bdc-overview.md)を参照してください。

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
