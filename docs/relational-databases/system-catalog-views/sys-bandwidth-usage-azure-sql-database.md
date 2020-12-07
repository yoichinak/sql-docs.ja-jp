---
description: sys.bandwidth_usage (Azure SQL Database)
title: bandwidth_usage (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d39486a513e012fc53e66c408145bbf148696ff2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88402528"
---
# <a name="sysbandwidth_usage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

> [!NOTE]
> これは、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11. * * にのみ適用されます。  
  
 ** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11 データベースサーバー**の各データベースによって使用されるネットワーク帯域幅に関する情報を返します。 指定のデータベースに対して返される各行は、1 時間にわたる 1 つの方向とクラスの使用状況をまとめたものです。  
  
 **このは、では非推奨とされました [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。**  
  
 **Bandwidth_usage**ビューには、次の列が含まれています。  
  
|列名|説明|  
|-----------------|-----------------|  
|**time**|帯域幅が使用されていた時間。 このビューの行は、1 時間単位です。 たとえば、2009-09-19 02:00: 00.000 は、帯域幅が 2009 年 9 月 19 日午前 2:00 から午前 3:00 までの間に使用された ことを示します。|  
|**database_name**|帯域幅を使用したデータベースの名前。|  
|**direction**|使用された帯域幅の種類で、次のいずれかになります。<br /><br /> 受信: に移動するデータ [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。<br /><br /> 送信: から移動するデータ [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。|  
|**class**|使用された帯域幅のクラス。次のどちらかです。<br />内部: Azure platform 内で移動するデータ。<br />外部: Azure platform から移行するデータ。<br /><br /> このクラスは、データベースで、地域 ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]) 間の連続コピー リレーションシップが進行中である場合に返されます。 特定のデータベースが連続コピーリレーションシップに含まれていない場合、"インターリンク" 行は返されません。 詳細については、後の「解説」を参照してください。|  
|**time_period**|使用が発生した時間帯は、Peak または OffPeak です。 Peak 時間は、サーバーが作成された地域に基づいています。 たとえば、 サーバーが "US_Northwest" リージョンで作成された場合、Peak 時間帯は太平洋標準時の午前 10:00 から 午後 6 時まで  (太平洋標準時)。|  
|**quantity**|使用された帯域幅の量 (KB 単位)。|  
  
## <a name="permissions"></a>アクセス許可

 このビューは、サーバーレベルプリンシパルログインの **master** データベースでのみ使用できます。  
  
## <a name="remarks"></a>解説  
  
### <a name="external-and-internal-classes"></a>外部クラスと内部クラス

 特定の時点で使用される各データベースについて、bandwidth_usage ビューは、クラスと帯域幅の使用状況の方向を示す行を返します **。** 次の例は、指定されたデータベースに対して公開される可能性があるデータを示しています。 この例では、時刻は 2012-04-21 17:00:00 になっています。これは、ピーク タイムの時間帯における発生時刻です。 データベース名は Db1 です。 この例では、次のように、 **bandwidth_usage** は、受信方向と送信方向、外部クラスと内部クラスの4つの組み合わせすべてに対して行を返しました。  
  
|time|database_name|方向|class|time_period|数量|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|イングレス|外部|Peak|66|  
|2012-04-21 17:00:00|Db1|エグレス|外部|Peak|741|  
|2012-04-21 17:00:00|Db1|イングレス|内部|Peak|1052|  
|2012-04-21 17:00:00|Db1|エグレス|内部|Peak|3525|  
  
### <a name="interpreting-data-direction-for-ssgeodr"></a>[!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]でのデータ方向の解釈

 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]の場合、帯域幅の使用状況データは連続コピー リレーションシップの両側にある論理マスター データベースで確認できます。 そのため、クエリを実行するデータベースの観点から、受信方向と送信方向のインジケーターを解釈する必要があります。 たとえば、ソース サーバーからターゲット サーバーへ、1 MB のデータを転送するレプリケーション ストリームについて考えてみます。 この場合、移行元サーバーでは、送信されたデータの合計に 1 MB がカウントされ、ターゲットサーバーでは、1 MB が受信データとして記録されます。  
  
> [!NOTE]  
> 転送されるデータの量は、転送元サーバーから対象サーバーまで、ユーザーデータフローの方向になります。 ただし、一部のデータ転送では他の方向が必要になる場合があります。  
